# Resource: aws_route_table

Provides a resource to create a VPC routing table.

## Basic Example

```yaml
resource:
  aws_route_table:
    example:
      vpc_id: ${aws_vpc.example.id}
      route:
        cidr_block: 10.0.1.0/24
        gateway_id: ${aws_internet_gateway.example.id}
      route:
        ipv6_cidr_block: "::/0"
        egress_only_gateway_id: ${aws_egress_only_internet_gateway.example.id}
      tags:
        Name: example
```

## Adopting an existing local route

```yaml
resource:
  aws_vpc:
    test:
      cidr_block: 10.1.0.0/16

resource:
  aws_route_table:
    test:
      vpc_id: ${aws_vpc.test.id}
      route:
        cidr_block: 10.1.0.0/16
        gateway_id: local
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_id` - (Required) The VPC ID.
* `route` - (Optional) A list of route objects. Their keys are documented below. This argument is processed in attribute-as-blocks mode.
This means that omitting this argument is interpreted as ignoring any existing routes. To remove all managed routes an empty list should be specified. See the example above.

* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `propagating_vgws` - (Optional) A list of virtual gateways for propagation.

### route Argument Reference

This argument is processed in attribute-as-blocks mode.

One of the following destination arguments must be supplied:

* `cidr_block` - (Required) The CIDR block of the route.
* `ipv6_cidr_block` - (Optional) The Ipv6 CIDR block of the route.
* `destination_prefix_list_id` - (Optional) The ID of a [managed prefix list](ec2_managed_prefix_list.html) destination of the route.

One of the following target arguments must be supplied:

* `carrier_gateway_id` - (Optional) Identifier of a carrier gateway. This attribute can only be used when the VPC contains a subnet which is associated with a Wavelength Zone.
* `core_network_arn` - (Optional) The Amazon Resource Name (ARN) of a core network.
* `egress_only_gateway_id` - (Optional) Identifier of a VPC Egress Only Internet Gateway.
* `gateway_id` - (Optional) Identifier of a VPC internet gateway, virtual private gateway, or `local`. `local` routes cannot be created but can be adopted or imported. See the [example](#adopting-an-existing-local-route) above.
* `local_gateway_id` - (Optional) Identifier of a Outpost local gateway.
* `nat_gateway_id` - (Optional) Identifier of a VPC NAT gateway.
* `network_interface_id` - (Optional) Identifier of an EC2 network interface.
* `transit_gateway_id` - (Optional) Identifier of an EC2 Transit Gateway.
* `vpc_endpoint_id` - (Optional) Identifier of a VPC Endpoint.
* `vpc_peering_connection_id` - (Optional) Identifier of a VPC peering connection.

Note that the default route, mapping the VPC's CIDR block to "local", is created implicitly and cannot be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the routing table.
* `arn` - The ARN of the route table.
* `owner_id` - The ID of the AWS account that owns the route table.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `2m`)
- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_route_table.public_rt rtb-4e616f6d69
```
