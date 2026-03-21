# Resource: aws_ssoadmin_application_assignment

ytofu resource for managing an AWS SSO Admin Application Assignment.

## Basic Example

```yaml
resource:
  aws_ssoadmin_application_assignment:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      principal_id: ${aws_identitystore_user.example.user_id}
      principal_type: USER
```

## Group Type

```yaml
resource:
  aws_ssoadmin_application_assignment:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      principal_id: ${aws_identitystore_group.example.group_id}
      principal_type: GROUP
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_arn` - (Required) ARN of the application.
* `principal_id` - (Required) An identifier for an object in IAM Identity Center, such as a user or group.
* `principal_type` - (Required) Entity type for which the assignment will be created. Valid values are `USER` or `GROUP`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A comma-delimited string concatenating `application_arn`, `principal_id`, and `principal_type`.

## Import

```bash
ytofu import aws_ssoadmin_application_assignment.example arn:aws:sso::123456789012:application/id-12345678,abcd1234,USER
```
