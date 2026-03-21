# Organizations Policy Attachment

Attach policies to OUs and accounts using ytofu YAML.

## Attach to OU

```yaml
resource:
  aws_organizations_policy_attachment:
    production:
      policy_id: ${aws_organizations_policy.deny_regions.id}
      target_id: ${aws_organizations_organizational_unit.production.id}
```

## Attach to Account

```yaml
resource:
  aws_organizations_policy_attachment:
    account:
      policy_id: ${aws_organizations_policy.deny_regions.id}
      target_id: ${aws_organizations_account.account.id}
```
