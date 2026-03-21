# DB Subnet Group

Manage DB Subnet Group resources using ytofu YAML.

## Basic Example

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
