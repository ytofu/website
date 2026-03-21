# Internet Gateway

Manage Internet Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_internet_gateway:
    gw:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main
```
