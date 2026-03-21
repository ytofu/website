# Neptune Subnet Group

Manage Neptune Subnet Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_neptune_subnet_group:
    default:
      name: main
      subnet_ids: 
        - ${aws_subnet.frontend.id}
        - ${aws_subnet.backend.id}
      tags:
        Name: My neptune subnet group
```
