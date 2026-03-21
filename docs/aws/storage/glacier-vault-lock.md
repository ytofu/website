# Resource: aws_glacier_vault_lock

Manages a Glacier Vault Lock. You can refer to the [Glacier Developer Guide](https://docs.aws.amazon.com/amazonglacier/latest/dev/vault-lock.html) for a full explanation of the Glacier Vault Lock functionality.

## Basic Example

```yaml
resource:
  aws_glacier_vault:
    example:
      name: example

  aws_glacier_vault_lock:
    example:
      complete_lock: false
      policy: ${data.aws_iam_policy_document.example.json}
      vault_name: ${aws_glacier_vault.example.name}

data:
  aws_iam_policy_document:
    example:
      statement:
        actions: 
          - "glacier:DeleteArchive"
        effect: Deny
        resources: 
          - ${aws_glacier_vault.example.arn}
        condition:
          test: NumericLessThanEquals
          values: 
            - 365```

## Permanently Applying Glacier Vault Lock Policy

```yaml
resource:
  aws_glacier_vault_lock:
    example:
      complete_lock: true
      policy: ${data.aws_iam_policy_document.example.json}
      vault_name: ${aws_glacier_vault.example.name}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `complete_lock` - (Required) Boolean whether to permanently apply this Glacier Lock Policy. Once completed, this cannot be undone. If set to `false`, the Glacier Lock Policy remains in a testing mode for 24 hours. After that time, the Glacier Lock Policy is automatically removed by Glacier and the ytofu resource will show as needing recreation. Changing this from `false` to `true` will show as resource recreation, which is expected. Changing this from `true` to `false` is not possible unless the Glacier Vault is recreated at the same time.
* `policy` - (Required) JSON string containing the IAM policy to apply as the Glacier Vault Lock policy.
* `vault_name` - (Required) The name of the Glacier Vault.
* `ignore_deletion_error` - (Optional) Allow ytofu to ignore the error returned when attempting to delete the Glacier Lock Policy. This can be used to delete or recreate the Glacier Vault via ytofu, for example, if the Glacier Vault Lock policy permits that action. This should only be used in conjunction with `complete_lock` being set to `true`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Glacier Vault name.

## Import

```bash
ytofu import aws_glacier_vault_lock.example example-vault
```
