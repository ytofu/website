# Route Table Association

Manage Route Table Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route_table_association:
    a:
      subnet_id: ${aws_subnet.foo.id}
      route_table_id: ${aws_route_table.bar.id}
```
