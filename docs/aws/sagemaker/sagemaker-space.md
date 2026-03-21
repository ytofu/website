# Sagemaker Space

Manage Sagemaker Space resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_space:
    example:
      domain_id: ${aws_sagemaker_domain.test.id}
      space_name: example
```
