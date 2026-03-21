# Resource: aws_organizations_account

Provides a resource to create a member account in the current organization.

## Basic Example

```yaml
resource:
  aws_organizations_account:
    account:
      name: my_new_account
      email: john@doe.org
```

## Argument Reference

The following arguments are required:

* `email` - (Required) Email address of the owner to assign to the new member account. This email address must not already be associated with another AWS account.
* `name` - (Required) Friendly name for the member account.

The following arguments are optional:

* `close_on_deletion` - (Optional) If true, a deletion event will close the account. Otherwise, it will only remove from the organization. This is not supported for GovCloud accounts.
* `create_govcloud` - (Optional) Whether to also create a GovCloud account. The GovCloud account is tied to the main (commercial) account this resource creates. If `true`, the GovCloud account ID is available in the `govcloud_id` attribute. The only way to manage the GovCloud account with ytofu is to subsequently import the account using this resource.
* `iam_user_access_to_billing` - (Optional) If set to `ALLOW`, the new account enables IAM users and roles to access account billing information if they have the required permissions. If set to `DENY`, then only the root user (and no roles) of the new account can access account billing information. If this is unset, the AWS API will default this to `ALLOW`. If the resource is created and this option is changed, it will try to recreate the account.
* `parent_id` - (Optional) Parent Organizational Unit ID or Root ID for the account. Defaults to the Organization default Root ID. A configuration must be present for this argument to perform drift detection.
* `role_name` - (Optional) The name of an IAM role that Organizations automatically preconfigures in the new member account. This role trusts the root account, allowing users in the root account to assume the role, as permitted by the root account administrator. The role has administrator permissions in the new member account. The Organizations API provides no method for reading this information after account creation, so ytofu cannot perform drift detection on its value and will always show a difference for a configured value after import unless `ignore_changes` is used.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN for this account.
* `govcloud_id` - ID for a GovCloud account created with the account.
* `id` - AWS account ID.
* `joined_method` - Method by which the account joined the organization.
* `joined_timestamp` - Date the account became a part of the organization.
* `state` - State of the account in the organization.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `update` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_organizations_account.example 111111111111
```
