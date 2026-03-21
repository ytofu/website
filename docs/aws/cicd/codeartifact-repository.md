# Codeartifact Repository

Manage Codeartifact Repository resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: domain key

resource:
  aws_codeartifact_domain:
    example:
      domain: example
      encryption_key: ${aws_kms_key.example.arn}

resource:
  aws_codeartifact_repository:
    test:
      repository: example
      domain: ${aws_codeartifact_domain.example.domain}
```
