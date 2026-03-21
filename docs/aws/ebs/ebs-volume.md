# EBS Volume

Manage EBS Volume resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ebs_volume:
    example:
      availability_zone: us-west-2a
      size: 40
      tags:
        Name: HelloWorld
```
