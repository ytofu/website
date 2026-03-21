# Macie2 Organization Admin Account

Manage Macie2 Organization Admin Account resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_macie2_account:
    example:

resource:
  aws_macie2_organization_admin_account:
    example:
      admin_account_id: ID OF THE ADMIN ACCOUNT
      depends_on: 
        - ${aws_macie2_account.example}
```
