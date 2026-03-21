# Resource: aws_ec2_transit_gateway_peering_attachment

Manages an EC2 Transit Gateway Peering Attachment.
For examples of custom route table association and propagation, see the [EC2 Transit Gateway Networking Examples Guide](https://docs.aws.amazon.com/vpc/latest/tgw/TGW_Scenarios.html).

## Basic Example

```yaml
data:
  aws_region:
    peer:

resource:
  aws_ec2_transit_gateway:
    local:
      tags:
        Name: Local TGW

resource:
  aws_ec2_transit_gateway:
    peer:
      tags:
        Name: Peer TGW

resource:
  aws_ec2_transit_gateway_peering_attachment:
    example:
      peer_account_id: ${aws_ec2_transit_gateway.peer.owner_id}
      peer_region: ${data.aws_region.peer.name}
      peer_transit_gateway_id: ${aws_ec2_transit_gateway.peer.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.local.id}
      tags:
        Name: TGW Peering Requestor
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `peer_account_id` - (Optional) Account ID of EC2 Transit Gateway to peer with. Defaults to the account ID the [AWS provider][1] is currently connected to.
* `peer_region` - (Required) Region of EC2 Transit Gateway to peer with.
* `peer_transit_gateway_id` - (Required) Identifier of EC2 Transit Gateway to peer with.
* `options` - (Optional) Describes whether dynamic routing is enabled or disabled for the transit gateway peering request. See [options](#options) below for more details!
* `tags` - (Optional) Key-value tags for the EC2 Transit Gateway Peering Attachment. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `transit_gateway_id` - (Required) Identifier of EC2 Transit Gateway.

### options

The `options` block supports the following:

* `dynamic_routing` - (Optional) Indicates whether dynamic routing is enabled or disabled.. Supports `enable` and `disable`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the attachment.
* `id` - EC2 Transit Gateway Attachment identifier.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_ec2_transit_gateway_peering_attachment.example tgw-attach-12345678
```
