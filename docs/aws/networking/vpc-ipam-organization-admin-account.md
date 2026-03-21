# VPC Ipam Organization Admin Account

Manage VPC Ipam Organization Admin Account resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_ipam_organization_admin_account:
    example:
      delegated_admin_account_id: ${data.aws_caller_identity.delegated.account_id}

data:
  aws_caller_identity:
    delegated:
```
