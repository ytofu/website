# SSM Document

Manage SSM Document resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssm_document:
    foo:
      name: test_document
      document_type: Command
      content: |
        {
        "schemaVersion": "1.2",
        "description": "Check ip configuration of a Linux instance.",
        "parameters": {
        
        },
        "runtimeConfig": {
        "aws:runShellScript": {
        "properties": [
        {
        "id": "0.aws:runShellScript",
        "runCommand": ["ifconfig"]
        }
        ]
        }
        }
        }
```

## Create an ssm document in YAML format

```yaml
resource:
  aws_ssm_document:
    foo:
      name: test_document
      document_format: YAML
      document_type: Command
      content: |
        schemaVersion: '1.2'
        description: Check ip configuration of a Linux instance.
        parameters: {}
        runtimeConfig:
        'aws:runShellScript':
        properties:
        - id: '0.aws:runShellScript'
        runCommand:
        - ifconfig
```
