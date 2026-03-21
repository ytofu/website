# Resource: aws_ssoadmin_application_access_scope

ytofu resource for managing an AWS SSO Admin Application Access Scope.

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_ssoadmin_application:
    example:
      name: example
      application_provider_arn: "arn:aws:sso::aws:applicationProvider/custom"
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}

  aws_ssoadmin_application_access_scope:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      authorized_targets: 
        - "arn:aws:sso::123456789012:application/ssoins-123456789012/apl-123456789012"
      scope: "sso:account:access"```

## Argument Reference

The following arguments are required:

* `application_arn` - (Required) Specifies the ARN of the application with the access scope with the targets to add or update.
* `scope` - (Required) Specifies the name of the access scope to be associated with the specified targets.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `authorized_targets` - (Optional) Specifies an array list of ARNs that represent the authorized targets for this access scope.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A comma-delimited string concatenating `application_arn` and `scope`.

## Import

```bash
ytofu import aws_ssoadmin_application_access_scope.example arn:aws:sso::123456789012:application/ssoins-123456789012/apl-123456789012,sso:account:access
```
