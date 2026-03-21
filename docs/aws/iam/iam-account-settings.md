# IAM Account Settings

Configure IAM account-level settings using ytofu YAML.

## Password Policy

```yaml
resource:
  aws_iam_account_password_policy:
    strict:
      minimum_password_length: 14
      require_lowercase_characters: true
      require_numbers: true
      require_uppercase_characters: true
      require_symbols: true
      allow_users_to_change_password: true
      max_password_age: 90
      password_reuse_prevention: 24
```

## Account Alias

```yaml
resource:
  aws_iam_account_alias:
    alias:
      account_alias: my-account-alias
```
