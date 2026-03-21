# AMI From Instance

Manage AMI From Instance resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ami_from_instance:
    example:
      name: terraform-example
      source_instance_id: i-xxxxxxxx
```
