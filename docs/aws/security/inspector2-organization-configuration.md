# Inspector2 Organization Configuration

Manage Inspector2 Organization Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_inspector2_organization_configuration:
    example:
      auto_enable:
        ec2: true
        ecr: false
        code_repository: false
        lambda: true
        lambda_code: true
```
