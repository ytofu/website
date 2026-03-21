# Ephemeral Values

Ephemeral values are memory-only data that never persists to state or plan files. They're ideal for handling sensitive information that should not be stored.

## Overview

Some data should never be written to disk:
- Temporary credentials
- Session tokens
- One-time passwords
- Secrets fetched at runtime

Ephemeral values guarantee this data exists only in memory during execution.

## Ephemeral Resources

Define resources that produce ephemeral values:

```hcl
ephemeral "aws_secretsmanager_secret_version" "db_password" {
  secret_id = "prod/database/password"
}

resource "aws_db_instance" "main" {
  # ... other configuration ...
  password = ephemeral.aws_secretsmanager_secret_version.db_password.secret_string
}
```

The secret value is fetched at runtime and never stored in state.

## Ephemeral Outputs

Mark outputs as ephemeral to prevent them from being stored:

```hcl
output "temporary_token" {
  value     = ephemeral.aws_sts_session_token.main.session_token
  ephemeral = true
}
```

Ephemeral outputs:
- Are not written to state
- Cannot be used by other configurations via `terraform_remote_state`
- Are displayed during apply but not persisted

## Use Cases

### Database Passwords

Fetch passwords at runtime without storing them:

```hcl
ephemeral "aws_secretsmanager_secret_version" "db" {
  secret_id = "prod/database/master-password"
}

resource "aws_rds_cluster" "main" {
  master_password = ephemeral.aws_secretsmanager_secret_version.db.secret_string
  # ...
}
```

### Temporary AWS Credentials

Use temporary credentials that refresh on each run:

```hcl
ephemeral "aws_sts_assume_role" "deploy" {
  role_arn = "arn:aws:iam::123456789012:role/DeployRole"
}

provider "aws" {
  alias  = "deploy"
  region = "us-west-2"

  access_key = ephemeral.aws_sts_assume_role.deploy.access_key
  secret_key = ephemeral.aws_sts_assume_role.deploy.secret_key
  token      = ephemeral.aws_sts_assume_role.deploy.session_token
}
```

### API Keys

Fetch API keys without storing them in state:

```hcl
ephemeral "vault_generic_secret" "api_key" {
  path = "secret/data/api-keys/stripe"
}

resource "stripe_webhook" "main" {
  api_key = ephemeral.vault_generic_secret.api_key.data["key"]
  # ...
}
```

## Write-Only Attributes

Some resource attributes are write-only and behave similarly to ephemeral values:

```hcl
resource "aws_db_instance" "main" {
  # password is write-only - not stored in state after initial creation
  password = var.db_password
}
```

Write-only attributes:
- Are sent to the provider during create/update
- Are not stored in state
- Cannot be read back after creation

## Ephemeral Variables

Variables can be marked as ephemeral:

```hcl
variable "temporary_token" {
  type      = string
  ephemeral = true
}
```

Ephemeral variables:
- Cannot have default values
- Must be provided at runtime
- Are not stored in plan files

## Comparison with Sensitive Values

| Feature | Sensitive | Ephemeral |
|---------|-----------|-----------|
| Masked in output | Yes | Yes |
| Stored in state | Yes (encrypted if configured) | No |
| Stored in plan | Yes | No |
| Can reference in resources | Yes | Yes |
| Can use in `count`/`for_each` | Yes | No |

Use **sensitive** when you need to store the value but hide it from logs.
Use **ephemeral** when the value should never be persisted.

## Limitations

Ephemeral values have some restrictions:

1. **Cannot be used in `count` or `for_each`** - The value must be known at plan time
2. **Cannot be used in `depends_on`** - Dependencies must be static
3. **Fetched on every run** - May increase API calls to secret managers
4. **Not available in state** - Cannot be referenced by other configurations

## Best Practices

1. **Use for true secrets** - Passwords, tokens, API keys that shouldn't be stored

2. **Combine with secret managers** - AWS Secrets Manager, HashiCorp Vault, Azure Key Vault

3. **Consider rotation** - Ephemeral values naturally support credential rotation

4. **Mind the API limits** - Fetching secrets on every run may hit rate limits

5. **Use encryption for persistent secrets** - If you must store secrets in state, use [encryption](encryption.md)

## Related

- [Encryption](encryption.md)
- [Resource Lifecycle](resource-lifecycle.md)
- [Configuration as Data](configuration-as-data.md)
