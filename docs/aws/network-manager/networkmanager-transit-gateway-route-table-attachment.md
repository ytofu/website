# Resource: aws_networkmanager_transit_gateway_route_table_attachment

Manages a Network Manager transit gateway route table attachment.

## Basic Example

```yaml
resource:
  aws_networkmanager_transit_gateway_route_table_attachment:
    example:
      peering_id: ${aws_networkmanager_transit_gateway_peering.example.id}
      transit_gateway_route_table_arn: ${aws_ec2_transit_gateway_route_table.example.arn}
```

## Argument Reference

The following arguments are required:

* `peering_id` - (Required) ID of the peer for the attachment.
* `transit_gateway_route_table_arn` - (Required) ARN of the transit gateway route table for the attachment.

The following arguments are optional:

* `routing_policy_label` - (Optional) The routing policy label to apply to the Transit Gateway route table attachment for traffic routing decisions. Maximum length of 256 characters. Changing this value will force recreation of the resource.
* `tags` - (Optional) Key-value tags for the attachment. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Attachment ARN.
* `attachment_policy_rule_number` - Policy rule number associated with the attachment.
* `attachment_type` - Type of attachment.
* `core_network_arn` - ARN of the core network.
* `core_network_id` - ID of the core network.
* `edge_location` - Edge location for the peer.
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

## Import

```bash
ytofu import aws_networkmanager_transit_gateway_route_table_attachment.example attachment-0f8fa60d2238d1bd8
```
