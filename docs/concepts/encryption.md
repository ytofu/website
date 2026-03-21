# State and Plan Encryption

ytofu supports encrypting state files and plan files at rest, protecting sensitive infrastructure data from unauthorized access.

## Overview

State files often contain sensitive information:
- Database passwords
- API keys
- Private IP addresses
- Resource configurations

Encryption ensures this data is protected when stored locally or in remote backends.

## Encryption Configuration

Configure encryption in your `terraform` block:

```hcl
terraform {
  encryption {
    key_provider "aws_kms" "main" {
      kms_key_id = "alias/ytofu-state"
      region     = "us-west-2"
    }

    method "aes_gcm" "default" {
      keys = key_provider.aws_kms.main
    }

    state {
      method = method.aes_gcm.default
    }

    plan {
      method = method.aes_gcm.default
    }
  }
}
```

## Key Providers

ytofu supports multiple key providers for different environments.

### AWS KMS

Use AWS Key Management Service for key management:

```hcl
key_provider "aws_kms" "main" {
  kms_key_id = "alias/ytofu-state"
  region     = "us-west-2"

  # Optional: use a specific AWS profile
  profile = "production"
}
```

Required IAM permissions:
- `kms:Encrypt`
- `kms:Decrypt`
- `kms:GenerateDataKey`

### Azure Key Vault

Use Azure Key Vault for key management:

```hcl
key_provider "azurerm_key_vault" "main" {
  key_vault_id = "/subscriptions/.../resourceGroups/.../providers/Microsoft.KeyVault/vaults/my-vault"
  key_name     = "ytofu-state-key"
}
```

### GCP Cloud KMS

Use Google Cloud KMS for key management:

```hcl
key_provider "gcp_kms" "main" {
  kms_encryption_key = "projects/my-project/locations/us/keyRings/my-ring/cryptoKeys/my-key"
}
```

### Local Passphrase

Use a local passphrase for simple encryption (suitable for development):

```hcl
key_provider "pbkdf2" "main" {
  passphrase = var.encryption_passphrase
}
```

Or use an environment variable:

```hcl
key_provider "pbkdf2" "main" {
  passphrase = env.TF_ENCRYPTION_PASSPHRASE
}
```

## Encryption Methods

### AES-GCM

The recommended encryption method using AES in Galois/Counter Mode:

```hcl
method "aes_gcm" "default" {
  keys = key_provider.aws_kms.main
}
```

## Encrypting State

Apply encryption to state files:

```hcl
encryption {
  # ... key_provider and method configuration ...

  state {
    method = method.aes_gcm.default

    # Optional: enforce encryption (fail if unencrypted state is found)
    enforced = true
  }
}
```

## Encrypting Plans

Apply encryption to plan files:

```hcl
encryption {
  # ... key_provider and method configuration ...

  plan {
    method = method.aes_gcm.default

    # Optional: enforce encryption
    enforced = true
  }
}
```

## Remote State Encryption

Configure encryption for reading remote state:

```hcl
encryption {
  # ... key_provider and method configuration ...

  remote_state_data_sources {
    default {
      method = method.aes_gcm.default
    }
  }
}
```

## Migration from Unencrypted State

When migrating existing unencrypted state to encrypted:

```hcl
encryption {
  key_provider "aws_kms" "main" {
    kms_key_id = "alias/ytofu-state"
    region     = "us-west-2"
  }

  method "aes_gcm" "default" {
    keys = key_provider.aws_kms.main
  }

  state {
    method = method.aes_gcm.default

    # Allow reading unencrypted state during migration
    fallback {}
  }
}
```

After running `ytofu apply`, the state will be encrypted. Then remove the `fallback` block:

```hcl
state {
  method   = method.aes_gcm.default
  enforced = true  # Now require encryption
}
```

## Complete Example

```hcl
terraform {
  encryption {
    # AWS KMS key provider
    key_provider "aws_kms" "production" {
      kms_key_id = "alias/ytofu-prod"
      region     = "us-west-2"
    }

    # AES-GCM encryption method
    method "aes_gcm" "secure" {
      keys = key_provider.aws_kms.production
    }

    # Encrypt state files
    state {
      method   = method.aes_gcm.secure
      enforced = true
    }

    # Encrypt plan files
    plan {
      method   = method.aes_gcm.secure
      enforced = true
    }

    # Encrypt remote state access
    remote_state_data_sources {
      default {
        method = method.aes_gcm.secure
      }
    }
  }

  backend "s3" {
    bucket = "my-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-west-2"
  }
}
```

## Best Practices

1. **Use cloud KMS in production** - AWS KMS, Azure Key Vault, or GCP KMS provide better key management than local passphrases

2. **Enforce encryption** - Set `enforced = true` to prevent accidental unencrypted state

3. **Rotate keys regularly** - Follow your organization's key rotation policies

4. **Separate keys per environment** - Use different encryption keys for dev, staging, and production

5. **Backup key access** - Ensure multiple team members can access encryption keys

## Troubleshooting

### Cannot decrypt state

If you see decryption errors:

1. Verify key provider credentials (AWS credentials, Azure identity, etc.)
2. Check key permissions
3. Ensure the correct key is configured
4. Verify the encryption method matches

### Migration issues

If migration from unencrypted state fails:

1. Add a `fallback {}` block to allow reading unencrypted state
2. Run `ytofu apply` to encrypt
3. Remove the `fallback {}` block
4. Set `enforced = true`

## Related

- [Resource Lifecycle](resource-lifecycle.md)
- [Configuration as Data](configuration-as-data.md)
