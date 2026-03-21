# Resource: aws_licensemanager_grant_accepter

Accepts a License Manager grant. This allows for sharing licenses with other aws accounts.

## Basic Example

```yaml
resource:
  aws_licensemanager_grant_accepter:
    test:
      grant_arn: "arn:aws:license-manager::123456789012:grant:g-1cf9fba4ba2f42dcab11c686c4b4d329"
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `grant_arn` - (Required) The ARN of the grant to accept.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The grant ARN (Same as `arn`).
* `arn` - The grant ARN.
* `name` - The Name of the grant.
* `allowed_operations` - A list of the allowed operations for the grant.
* `license_arn` - The ARN of the license for the grant.
* `principal` - The target account for the grant.
* `home_region` - The home region for the license.
* `parent_arn` - The parent ARN.
* `status` - The grant status.
* `version` - The grant version.

## Import

```bash
ytofu import aws_licensemanager_grant_accepter.test arn:aws:license-manager::123456789012:grant:g-1cf9fba4ba2f42dcab11c686c4b4d329
```
