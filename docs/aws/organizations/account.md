# AWS Organizations Account

Create member accounts using ytofu YAML.

## Basic Account

```yaml
resource:
  aws_organizations_account:
    account:
      name: my-new-account
      email: admin@example.com
```

## With Parent OU

```yaml
resource:
  aws_organizations_account:
    account:
      name: production-account
      email: prod@example.com
      parent_id: ${aws_organizations_organizational_unit.production.id}
      role_name: OrganizationAccountAccessRole
      tags:
        Environment: production
```
