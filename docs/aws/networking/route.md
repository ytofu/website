# Resource: aws_route

Provides a resource to create a routing table entry (a route) in a VPC routing table.

## Basic Example

```yaml
resource:
  aws_route:
    r:
      route_table_id: ${aws_route_table.testing.id}
      destination_cidr_block: 10.0.1.0/22
      vpc_peering_connection_id: pcx-45ff3dc1
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `route_table_id` - (Required) The ID of the routing table.

One of the following destination arguments must be supplied:

* `destination_cidr_block` - (Optional) The destination CIDR block.
* `destination_ipv6_cidr_block` - (Optional) The destination IPv6 CIDR block.
* `destination_prefix_list_id` - (Optional) The ID of a [managed prefix list](ec2_managed_prefix_list.html) destination.

One of the following target arguments must be supplied:

* `carrier_gateway_id` - (Optional) Identifier of a carrier gateway. This attribute can only be used when the VPC contains a subnet which is associated with a Wavelength Zone.
* `core_network_arn` - (Optional) The Amazon Resource Name (ARN) of a core network.
* `egress_only_gateway_id` - (Optional) Identifier of a VPC Egress Only Internet Gateway.
* `gateway_id` - (Optional) Identifier of a VPC internet gateway or a virtual private gateway. Specify `local` when updating a previously [imported](#import) local route.
* `nat_gateway_id` - (Optional) Identifier of a VPC NAT gateway.
* `local_gateway_id` - (Optional) Identifier of a Outpost local gateway.
* `network_interface_id` - (Optional) Identifier of an EC2 network interface.
* `transit_gateway_id` - (Optional) Identifier of an EC2 Transit Gateway.
* `vpc_endpoint_id` - (Optional) Identifier of a VPC Endpoint.
* `vpc_peering_connection_id` - (Optional) Identifier of a VPC peering connection.

Note that the default route, mapping the VPC's CIDR block to "local", is created implicitly and cannot be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Route identifier computed from the routing table identifier and route destination.
* `instance_id` - Identifier of an EC2 instance.
* `instance_owner_id` - The AWS account ID of the owner of the EC2 instance.
* `origin` - How the route was created - `CreateRouteTable`, `CreateRoute` or `EnableVgwRoutePropagation`.
* `state` - The state of the route - `active` or `blackhole`.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `2m`)
- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_route.my_route rtb-656C65616E6F72_10.42.0.0/16
```
