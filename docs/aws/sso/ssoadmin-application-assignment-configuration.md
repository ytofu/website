# Resource: aws_ssoadmin_application_assignment_configuration

ytofu resource for managing an AWS SSO Admin Application Assignment Configuration.

## Basic Example

```yaml
resource:
  aws_ssoadmin_application_assignment_configuration:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      assignment_required: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_arn` - (Required) ARN of the application.
* `assignment_required` - (Required) Indicates whether users must have an explicit assignment to access the application. If `false`, all users have access to the application.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ARN of the application.

## Import

```bash
ytofu import aws_ssoadmin_application_assignment_configuration.example arn:aws:sso::123456789012:application/id-12345678
```
