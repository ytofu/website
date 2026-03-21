# Auditmanager Framework Share

Manage Auditmanager Framework Share resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_auditmanager_framework_share:
    example:
      destination_account: 123456789012
      destination_region: us-east-1
      framework_id: ${aws_auditmanager_framework.example.id}
```
