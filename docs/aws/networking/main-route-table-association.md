# Main Route Table Association

Manage Main Route Table Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_main_route_table_association:
    a:
      vpc_id: ${aws_vpc.foo.id}
      route_table_id: ${aws_route_table.bar.id}
```
