# Datazone User Profile

Manage Datazone User Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datazone_user_profile:
    example:
      user_identifier: ${aws_iam_user.example.arn}
      domain_identifier: ${aws_datazone_domain.example.id}
      user_type: IAM_USER
```
