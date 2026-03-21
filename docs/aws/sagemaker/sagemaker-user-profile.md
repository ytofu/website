# Sagemaker User Profile

Manage Sagemaker User Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_user_profile:
    example:
      domain_id: ${aws_sagemaker_domain.test.id}
      user_profile_name: example
```
