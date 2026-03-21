# Resource: aws_inspector2_member_association

ytofu resource for associating accounts to existing Inspector instances.

## Basic Example

```yaml
resource:
  aws_inspector2_member_association:
    example:
      account_id: 123456789012
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Required) ID of the account to associate

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `delegated_admin_account_id` - Account ID of the delegated administrator account
* `relationship_status` - Status of the member relationship
* `updated_at` - Date and time of the last update of the relationship

## Import

```bash
ytofu import aws_inspector2_member_association.example 123456789012
```
