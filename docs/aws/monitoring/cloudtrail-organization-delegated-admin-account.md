# Cloudtrail Organization Delegated Admin Account

Manage Cloudtrail Organization Delegated Admin Account resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudtrail_organization_delegated_admin_account:
    example:
      account_id: ${data.aws_caller_identity.delegated.account_id}

data:
  aws_caller_identity:
    delegated:
```
