# Resource: aws_networkmanager_site_to_site_vpn_attachment

Manages a Network Manager site-to-site VPN attachment.

## Basic Example

```yaml
resource:
  aws_networkmanager_site_to_site_vpn_attachment:
    example:
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpn_connection_arn: ${aws_vpn_connection.example.arn}
```

## Full Usage

```yaml
resource:
  aws_customer_gateway:
    test:
      bgp_asn: 65000
      ip_address: 172.0.0.1
      type: ipsec.1

resource:
  aws_vpn_connection:
    test:
      customer_gateway_id: ${aws_customer_gateway.test.id}
      type: ipsec.1
      tags:
        Name: test

resource:
  aws_networkmanager_global_network:
    test:
      tags:
        Name: test

resource:
  awscc_networkmanager_core_network:
    test:
      global_network_id: ${aws_networkmanager_global_network.test.id}
      policy_document: example-value

data:
  aws_networkmanager_core_network_policy_document:
    test:
      core_network_configuration:
        vpn_ecmp_support: false
        asn_ranges: 
          - 64512-64555
        edge_locations:
          location: ${data.aws_region.current.region}
          asn: 64512
      segments:
        name: shared
        description: SegmentForSharedServices
        require_attachment_acceptance: true
      segment_actions:
        action: share
        mode: attachment-route
        segment: shared
        share_with: 
          - "*"
      attachment_policies:
        rule_number: 1
        condition_logic: or
        conditions:
          type: tag-value
          operator: equals
          key: segment
          value: shared
        action:
          association_method: constant
          segment: shared

resource:
  aws_networkmanager_site_to_site_vpn_attachment:
    test:
      core_network_id: ${awscc_networkmanager_core_network.test.id}
      vpn_connection_arn: ${aws_vpn_connection.test.arn}
      tags:
        segment: shared

resource:
  aws_networkmanager_attachment_accepter:
    test:
      attachment_id: ${aws_networkmanager_site_to_site_vpn_attachment.test.id}
      attachment_type: ${aws_networkmanager_site_to_site_vpn_attachment.test.attachment_type}
```

## Argument Reference

The following arguments are required:

* `core_network_id` - (Required) ID of a core network for the VPN attachment.
* `vpn_connection_arn` - (Required) ARN of the site-to-site VPN connection.

The following arguments are optional:

* `routing_policy_label` - (Optional) The routing policy label to apply to the Site-to-Site VPN attachment for traffic routing decisions. Maximum length of 256 characters. Changing this value will force recreation of the resource.
* `tags` - (Optional) Key-value tags for the attachment. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

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

* `create` - (Default `10m`)
* `delete` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_networkmanager_site_to_site_vpn_attachment.example attachment-0f8fa60d2238d1bd8
```
