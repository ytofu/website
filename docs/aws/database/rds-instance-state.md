# RDS Instance State

Manage RDS Instance State resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rds_instance_state:
    test:
      identifier: ${aws_db_instance.test.identifier}
      state: available
```
