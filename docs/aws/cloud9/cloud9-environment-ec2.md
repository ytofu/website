# Cloud9 Environment EC2

Manage Cloud9 Environment EC2 resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloud9_environment_ec2:
    example:
      instance_type: t2.micro
      name: example-env
      image_id: amazonlinux-2023-x86_64
```
