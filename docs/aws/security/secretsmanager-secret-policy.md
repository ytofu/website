# Secretsmanager Secret Policy

Manage Secretsmanager Secret Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: EnableAnotherAWSAccountToReadTheSecret
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "arn:aws:iam::123456789012:root"
        actions: 
          - "secretsmanager:GetSecretValue"
        resources: 
          - "*"

resource:
  aws_secretsmanager_secret_policy:
    example:
      secret_arn: ${aws_secretsmanager_secret.example.arn}
      policy: ${data.aws_iam_policy_document.example.json}
```
