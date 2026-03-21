# Finspace Kx Database

Manage Finspace Kx Database resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: Example KMS Key
      deletion_window_in_days: 7

resource:
  aws_finspace_kx_environment:
    example:
      name: my-tf-kx-environment
      kms_key_id: ${aws_kms_key.example.arn}

resource:
  aws_finspace_kx_database:
    example:
      environment_id: ${aws_finspace_kx_environment.example.id}
      name: my-tf-kx-database
      description: Example database description
```
