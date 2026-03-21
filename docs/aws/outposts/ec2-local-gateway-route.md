# Resource: aws_ec2_local_gateway_route

Manages an EC2 Local Gateway Route. More information can be found in the [Outposts User Guide](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-networking-components.html#routing).

## Basic Example

```yaml
resource:
  aws_ec2_local_gateway_route:
    example:
      destination_cidr_block: 172.16.0.0/16
      local_gateway_route_table_id: ${data.aws_ec2_local_gateway_route_table.example.id}
      local_gateway_virtual_interface_group_id: ${data.aws_ec2_local_gateway_virtual_interface_group.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `destination_cidr_block` - (Required) IPv4 CIDR range used for destination matches. Routing decisions are based on the most specific match.
* `local_gateway_route_table_id` - (Required) Identifier of EC2 Local Gateway Route Table.
* `local_gateway_virtual_interface_group_id` - (Required) Identifier of EC2 Local Gateway Virtual Interface Group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - EC2 Local Gateway Route Table identifier and destination CIDR block separated by underscores (`_`)

## Import

```bash
ytofu import aws_ec2_local_gateway_route.example lgw-rtb-12345678_172.16.0.0/16
```
