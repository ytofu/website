# Resource: aws_networkmanager_vpc_attachment

Manages a Network Manager VPC attachment.

## Basic Example

```yaml
resource:
  aws_networkmanager_vpc_attachment:
    example:
      subnet_arns: 
        - ${aws_subnet.example.arn}
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpc_arn: ${aws_vpc.example.arn}
```

## Usage with Options

```yaml
resource:
  aws_networkmanager_vpc_attachment:
    example:
      subnet_arns: 
        - ${aws_subnet.example.arn}
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpc_arn: ${aws_vpc.example.arn}
      options:
        appliance_mode_support: false
        dns_support: true
        ipv6_support: false
        security_group_referencing_support: true
```

## Argument Reference

The following arguments are required:

* `core_network_id` - (Required) ID of a core network for the VPC attachment.
* `subnet_arns` - (Required) Subnet ARNs of the VPC attachment.
* `vpc_arn` - (Required) ARN of the VPC.

The following arguments are optional:

* `options` - (Optional) Options for the VPC attachment. [See below](#options).
* `routing_policy_label` - (Optional) The routing policy label to apply to the VPC attachment for traffic routing decisions. Maximum length of 256 characters.
* `tags` - (Optional) Key-value tags for the attachment. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### options

* `appliance_mode_support` - (Optional) Whether to enable appliance mode support. If enabled, traffic flow between a source and destination use the same Availability Zone for the VPC attachment for the lifetime of that flow. If the VPC attachment is pending acceptance, changing this value will recreate the resource.
* `dns_support` - (Optional) Whether to enable DNS support. If the VPC attachment is pending acceptance, changing this value will recreate the resource.
* `ipv6_support` - (Optional) Whether to enable IPv6 support. If the VPC attachment is pending acceptance, changing this value will recreate the resource.
* `security_group_referencing_support` - (Optional) Whether to enable security group referencing support for this VPC attachment. The default is `true`. However, at the core network policy-level the default is set to `false`. If the VPC attachment is pending acceptance, changing this value will recreate the resource.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the attachment.
* `attachment_policy_rule_number` - Policy rule number associated with the attachment.
* `attachment_type` - Type of attachment.
* `core_network_arn` - ARN of a core network.
* `edge_location` - Region where the edge is located.
* `id` - ID of the attachment.
* `owner_account_id` - ID of the attachment account owner.
* `resource_arn` - Attachment resource ARN.
* `segment_name` - Name of the segment attachment.
* `state` - State of the attachment.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `15m`)
* `delete` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_networkmanager_vpc_attachment.example attachment-0f8fa60d2238d1bd8
```
