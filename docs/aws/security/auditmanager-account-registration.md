# Resource: aws_auditmanager_account_registration

ytofu resource for managing AWS Audit Manager Account Registration.

## Basic Example

```yaml
resource:
  aws_auditmanager_account_registration:
    example:
```

## Deregister On Destroy

```yaml
resource:
  aws_auditmanager_account_registration:
    example:
      deregister_on_destroy: true
```

## Argument Reference

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `delegated_admin_account` - (Optional) Identifier for the delegated administrator account.
* `deregister_on_destroy` - (Optional) Flag to deregister AuditManager in the account upon destruction. Defaults to `false` (ie. AuditManager will remain active in the account, even if this resource is removed).
* `kms_key` - (Optional) KMS key identifier.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Unique identifier for the account registration. Since registration is applied per AWS region, this will be the active region name (ex. `us-east-1`).
* `status` - Status of the account registration request.

## Import

```bash
ytofu import aws_auditmanager_account_registration.example us-east-1
```
