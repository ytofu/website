# EC2 Host

Manage EC2 Host resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_host:
    test:
      instance_type: c5.18xlarge
      availability_zone: us-west-2a
      host_recovery: on
      auto_placement: on
```
