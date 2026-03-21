# Resource: aws_vpn_gateway_route_propagation

Requests automatic route propagation between a VPN gateway and a route table.

## Basic Example

```yaml
resource:
  aws_vpn_gateway_route_propagation:
    example:
      vpn_gateway_id: ${aws_vpn_gateway.example.id}
      route_table_id: ${aws_route_table.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpn_gateway_id` - The id of the `aws_vpn_gateway` to propagate routes from.
* `route_table_id` - The id of the `aws_route_table` to propagate routes into.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

- `create` - (Default `2m`)
- `delete` - (Default `2m`)
