# Resource: aws_workmail_organization

Manages an AWS WorkMail Organization.

## Basic Example

```yaml
resource:
  aws_workmail_organization:
    example:
      organization_alias: example-org
```

## Argument Reference

The following arguments are required:

* `organization_alias` - (Required) Alias for the organization. Must be unique globally. Changing this creates a new resource.

The following arguments are optional:

* `delete_directory` - (Optional) Whether to delete the AWS Directory Service directory associated with the organization on destroy. To update this value after creation, run `ytofu apply` before running `ytofu destroy`. Defaults to `false`.
* `delete_identity_center_application` - Whether to delete the IAM Identity Center application associated with the organization on destroy. To update this value after creation, run `ytofu apply` before running `ytofu destroy`. Defaults to `false`.
* `directory_id` - (Optional) ID of an existing directory to associate with the organization. Changing this creates a new resource.
* `interoperability_enabled` - (Optional) Whether to enable interoperability between WorkMail and Microsoft Exchange. Changing this creates a new resource.
* `kms_key_arn` - (Optional) ARN of a customer-managed KMS key to encrypt the organization's data. If omitted, AWS managed keys are used. Changing this creates a new resource.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Organization.
* `completed_date` - Date and time (RFC3339) at which the organization became active.
* `default_mail_domain` - Default mail domain for the organization.
* `directory_type` - Type of the associated directory.
* `migration_admin` - User ID of the migration admin if migration is enabled.
* `organization_id` - ID of the WorkMail Organization.
* `state` - State of the organization.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_workmail_organization.example m-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
