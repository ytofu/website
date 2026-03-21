# Resource: aws_networkmanager_core_network_policy_attachment

Manages a Network Manager Core Network Policy Attachment.

## Basic Example

```yaml
resource:
  aws_networkmanager_core_network:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}

resource:
  aws_networkmanager_core_network_policy_attachment:
    example:
      core_network_id: ${aws_networkmanager_core_network.example.id}
      policy_document: ${data.aws_networkmanager_core_network_policy_document.example.json}
```

## With VPC Attachment (Single Region)

```yaml
resource:
  aws_networkmanager_global_network:
    example:

data:
  aws_networkmanager_core_network_policy_document:
    base:
      core_network_configuration:
        asn_ranges: 
          - 65022-65534
        edge_locations:
          location: us-west-2
          asn: 65500
      segments:
        name: segment

resource:
  aws_networkmanager_core_network:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      base_policy_document: ${data.aws_networkmanager_core_network_policy_document.base.json}
      create_base_policy: true

data:
  aws_networkmanager_core_network_policy_document:
    example:
      core_network_configuration:
        asn_ranges: 
          - 65022-65534
        edge_locations:
          location: us-west-2
          asn: 65500
      segments:
        name: segment
      segment_actions:
        action: create-route
        segment: segment
        destination_cidr_blocks:
          - 0.0.0.0/0
        destinations:
          - ${aws_networkmanager_vpc_attachment.example.id}

resource:
  aws_networkmanager_core_network_policy_attachment:
    example:
      core_network_id: ${aws_networkmanager_core_network.example.id}
      policy_document: ${data.aws_networkmanager_core_network_policy_document.example.json}

resource:
  aws_networkmanager_vpc_attachment:
    example:
      core_network_id: ${aws_networkmanager_core_network.example.id}
      subnet_arns: ${aws_subnet.example[*].arn}
      vpc_arn: ${aws_vpc.example.arn}
```

## With VPC Attachment (Multi-Region)

```yaml
resource:
  aws_networkmanager_global_network:
    example:

data:
  aws_networkmanager_core_network_policy_document:
    base:
      core_network_configuration:
        asn_ranges: 
          - 65022-65534
        edge_locations:
          location: us-west-2
          asn: 65500
        edge_locations:
          location: us-east-1
          asn: 65501
      segments:
        name: segment

resource:
  aws_networkmanager_core_network:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      base_policy_document: ${data.aws_networkmanager_core_network_policy_document.base.json}
      create_base_policy: true

data:
  aws_networkmanager_core_network_policy_document:
    example:
      core_network_configuration:
        asn_ranges: 
          - 65022-65534
        edge_locations:
          location: us-west-2
          asn: 65500
        edge_locations:
          location: us-east-1
          asn: 65501
      segments:
        name: segment
      segments:
        name: segment2
      segment_actions:
        action: create-route
        segment: segment
        destination_cidr_blocks:
          - 10.0.0.0/16
        destinations:
          - ${aws_networkmanager_vpc_attachment.example_us_west_2.id}
      segment_actions:
        action: create-route
        segment: segment
        destination_cidr_blocks:
          - 10.1.0.0/16
        destinations:
          - ${aws_networkmanager_vpc_attachment.example_us_east_1.id}

resource:
  aws_networkmanager_core_network_policy_attachment:
    example:
      core_network_id: ${aws_networkmanager_core_network.example.id}
      policy_document: ${data.aws_networkmanager_core_network_policy_document.example.json}

resource:
  aws_networkmanager_vpc_attachment:
    example_us_west_2:
      core_network_id: ${aws_networkmanager_core_network.example.id}
      subnet_arns: ${aws_subnet.example_us_west_2[*].arn}
      vpc_arn: ${aws_vpc.example_us_west_2.arn}

resource:
  aws_networkmanager_vpc_attachment:
    example_us_east_1:
      core_network_id: ${aws_networkmanager_core_network.example.id}
      subnet_arns: ${aws_subnet.example_us_east_1[*].arn}
      vpc_arn: ${aws_vpc.example_us_east_1.arn}
```

## Argument Reference

The following arguments are required:

* `core_network_id` - (Required) ID of the core network that a policy will be attached to and made `LIVE`.
* `policy_document` - (Required) Policy document for creating a core network. Note that updating this argument will result in the new policy document version being set as the `LATEST` and `LIVE` policy document. Refer to the [Core network policies documentation](https://docs.aws.amazon.com/network-manager/latest/cloudwan/cloudwan-policy-change-sets.html) for more information.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `state` - Current state of a core network.

## Timeouts

Configuration options:

* `update` - (Default `30m`). If this is the first time attaching a policy to a core network then this timeout value is also used as the `create` timeout value.

## Import

```bash
ytofu import aws_networkmanager_core_network_policy_attachment.example core-network-0d47f6t230mz46dy4
```
