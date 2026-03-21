# Sagemaker Code Repository

Manage Sagemaker Code Repository resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_code_repository:
    example:
      code_repository_name: example
      git_config:
        repository_url: "https://github.com/hashicorp/terraform-provider-aws.git"
```

## Example with Secret

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example

resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-json-policy

resource:
  aws_sagemaker_code_repository:
    example:
      code_repository_name: example
      git_config:
        repository_url: "https://github.com/hashicorp/terraform-provider-aws.git"
        secret_arn: ${aws_secretsmanager_secret.example.arn}
      depends_on: 
        - ${aws_secretsmanager_secret_version.example}
```
