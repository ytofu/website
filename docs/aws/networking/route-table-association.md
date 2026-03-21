# Resource: aws_route_table_association

Provides a resource to create an association between a route table and a subnet or a route table and an
internet gateway or virtual private gateway.

## Basic Example

```yaml
resource:
  aws_route_table_association:
    a:
      subnet_id: ${aws_subnet.foo.id}
      route_table_id: ${aws_route_table.bar.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `subnet_id` - (Optional) The subnet ID to create an association. Conflicts with `gateway_id`.
* `gateway_id` - (Optional) The gateway ID to create an association. Conflicts with `subnet_id`.
* `route_table_id` - (Required) The ID of the routing table to associate with.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the association

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `2m`)
- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_route_table_association.assoc subnet-6777656e646f6c796e/rtb-656c65616e6f72
```
