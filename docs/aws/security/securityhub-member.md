# Securityhub Member

Manage Securityhub Member resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_member:
    example:
      depends_on: 
        - ${aws_securityhub_account.example}
      account_id: 123456789012
      email: example@example.com
      invite: true
```
