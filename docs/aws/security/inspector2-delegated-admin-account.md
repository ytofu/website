# Inspector2 Delegated Admin Account

Manage Inspector2 Delegated Admin Account resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_inspector2_delegated_admin_account:
    example:
      account_id: ${data.aws_caller_identity.current.account_id}
```
