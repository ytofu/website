# Resource: aws_iam_user_login_profile

Manages an IAM User Login Profile with limited support for password creation during ytofu resource creation. Uses PGP to encrypt the password for safe transport to the user. PGP keys can be obtained from Keybase.

## Basic Example

```yaml
resource:
  aws_iam_user:
    example:
      name: example
      path: /
      force_destroy: true

  aws_iam_user_login_profile:
    example:
      user: ${aws_iam_user.example.name}
      pgp_key: "keybase:some_person_that_exists"

output:
  password:
    value: ${aws_iam_user_login_profile.example.encrypted_password}```

## Argument Reference

This resource supports the following arguments:

* `user` - (Required) The IAM user's name.
* `pgp_key` - (Optional) Either a base-64 encoded PGP public key, or a keybase username in the form `keybase:username`. Only applies on resource creation. Drift detection is not possible with this argument.
* `password_length` - (Optional) The length of the generated password on resource creation. Only applies on resource creation. Drift detection is not possible with this argument. Default value is `20`.
* `password_reset_required` - (Optional) Whether the user should be forced to reset the generated password on resource creation. Only applies on resource creation.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `password` - The plain text password, only available when `pgp_key` is not provided.
* `key_fingerprint` - The fingerprint of the PGP key used to encrypt the password. Only available if password was handled on ytofu resource creation, not import.
* `encrypted_password` - The encrypted password, base64 encoded. Only available if password was handled on ytofu resource creation, not import.

## Import

```bash
ytofu import aws_iam_user_login_profile.example myusername
```
