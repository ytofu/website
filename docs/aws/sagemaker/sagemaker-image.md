# Sagemaker Image

Manage Sagemaker Image resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_image:
    example:
      image_name: example
      role_arn: ${aws_iam_role.test.arn}
```
