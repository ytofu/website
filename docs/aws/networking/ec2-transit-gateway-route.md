# Resource: aws_ec2_transit_gateway_route

Manages an EC2 Transit Gateway Route.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_route:
    example:
      destination_cidr_block: 0.0.0.0/0
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway.example.association_default_route_table_id}
```

## Blackhole route

```yaml
resource:
  aws_ec2_transit_gateway_route:
    example:
      destination_cidr_block: 0.0.0.0/0
      blackhole: true
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway.example.association_default_route_table_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `destination_cidr_block` - (Required) IPv4 or IPv6 RFC1924 CIDR used for destination matches. Routing decisions are based on the most specific match.
* `transit_gateway_attachment_id` - (Optional) Identifier of EC2 Transit Gateway Attachment (required if `blackhole` is set to false).
* `blackhole` - (Optional) Indicates whether to drop traffic that matches this route (default to `false`).
* `transit_gateway_route_table_id` - (Required) Identifier of EC2 Transit Gateway Route Table.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - EC2 Transit Gateway Route Table identifier combined with destination

## Import

```bash
ytofu import aws_ec2_transit_gateway_route.example tgw-rtb-12345678_0.0.0.0/0
```
