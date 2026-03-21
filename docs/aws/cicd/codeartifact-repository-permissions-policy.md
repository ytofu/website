# Codeartifact Repository Permissions Policy

Manage Codeartifact Repository Permissions Policy resources using ytofu YAML.

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
    example:
      repository: example
      domain: ${aws_codeartifact_domain.example.domain}

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions: 
          - "codeartifact:ReadFromRepository"
        resources: 
          - ${aws_codeartifact_repository.example.arn}

resource:
  aws_codeartifact_repository_permissions_policy:
    example:
      repository: ${aws_codeartifact_repository.example.repository}
      domain: ${aws_codeartifact_domain.example.domain}
      policy_document: ${data.aws_iam_policy_document.example.json}
```
