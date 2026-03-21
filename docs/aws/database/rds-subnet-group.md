# RDS Subnet Group

Create DB subnet groups for RDS instances using ytofu YAML.

## Basic Subnet Group

```yaml
resource:
  aws_db_subnet_group:
    default:
      name: main
      subnet_ids:
        - ${aws_subnet.frontend.id}
        - ${aws_subnet.backend.id}
      tags:
        Name: My DB subnet group
```
