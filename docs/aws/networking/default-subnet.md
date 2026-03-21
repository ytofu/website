# Default Subnet

Manage Default Subnet resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_default_subnet:
    default_az1:
      availability_zone: us-west-2a
      tags:
        Name: Default subnet for us-west-2a
```
