# Codegurureviewer Repository Association

Manage Codegurureviewer Repository Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:

resource:
  aws_codecommit_repository:
    example:
      repository_name: example-repo
      lifecycle:
        ignore_changes:
          - tags["codeguru-reviewer"]

resource:
  aws_codegurureviewer_repository_association:
    example:
      repository:
        codecommit:
          name: ${aws_codecommit_repository.example.repository_name}
      kms_key_details:
        encryption_option: CUSTOMER_MANAGED_CMK
        kms_key_id: ${aws_kms_key.example.key_id}
```
