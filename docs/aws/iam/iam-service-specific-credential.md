# IAM Service Specific Credential

Manage IAM Service Specific Credential resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_user:
    example:
      name: example

resource:
  aws_iam_service_specific_credential:
    example:
      service_name: codecommit.amazonaws.com
      user_name: ${aws_iam_user.example.name}
```

## Bedrock API Key with Expiration

```yaml
resource:
  aws_iam_user:
    example:
      name: example

resource:
  aws_iam_service_specific_credential:
    bedrock:
      service_name: bedrock.amazonaws.com
      user_name: ${aws_iam_user.example.name}
      credential_age_days: 30
```
