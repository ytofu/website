# Resource: aws_networkmanager_transit_gateway_peering

Manages a Network Manager transit gateway peering connection. Creates a peering connection between an AWS Cloud WAN core network and an AWS Transit Gateway.

## Basic Example

```yaml
resource:
  aws_networkmanager_transit_gateway_peering:
    example:
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      transit_gateway_arn: ${aws_ec2_transit_gateway.example.arn}
      depends_on:
        - ${aws_ec2_transit_gateway_policy_table.example}
        - ${aws_networkmanager_core_network_policy_attachment.example}
```

## Argument Reference

The following arguments are required:

* `core_network_id` - (Required) ID of a core network.
* `transit_gateway_arn` - (Required) ARN of the transit gateway for the peering request.

The following arguments are optional:

* `tags` - (Optional) Key-value tags for the peering. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Peering ARN.
* `core_network_arn` - ARN of the core network.
* `edge_location` - Edge location for the peer.
* `id` - Peering ID.
* `owner_account_id` - ID of the account owner.
* `peering_type` - Type of peering. This will be `TRANSIT_GATEWAY`.
* `resource_arn` - Resource ARN of the peer.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `transit_gateway_peering_attachment_id` - ID of the transit gateway peering attachment.

## Timeouts

Configuration options:

* `create` - (Default `20m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_networkmanager_transit_gateway_peering.example peering-444555aaabbb11223
```
