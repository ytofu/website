# Devicefarm Test Grid Project

Manage Devicefarm Test Grid Project resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_devicefarm_test_grid_project:
    example:
      name: example
      vpc_config:
        vpc_id: ${aws_vpc.example.id}
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: ${aws_security_group.example[*].id}
```
