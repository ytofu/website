# Resource: aws_appconfig_extension_association

Associates an AppConfig Extension with a Resource.

## Basic Example

```yaml
resource:
  aws_sns_topic:
    test:
      name: test

  aws_iam_role:
    test:
      name: test
      assume_role_policy: ${data.aws_iam_policy_document.test.json}

  aws_appconfig_extension:
    test:
      name: test
      description: test description
      action_point:
        point: ON_DEPLOYMENT_COMPLETE
        action:
          name: test
          role_arn: ${aws_iam_role.test.arn}
          uri: ${aws_sns_topic.test.arn}
      tags:
        Type: AppConfig Extension

  aws_appconfig_application:
    test:
      name: test

  aws_appconfig_extension_association:
    test:
      extension_arn: ${aws_appconfig_extension.test.arn}
      resource_arn: ${aws_appconfig_application.test.arn}

data:
  aws_iam_policy_document:
    test:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - appconfig.amazonaws.com```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `extension_arn` - (Required) The ARN of the extension defined in the association.
* `resource_arn` - (Optional) The ARN of the application, configuration profile, or environment to associate with the extension.
* `parameters` - (Optional) The parameter names and values defined for the association.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the AppConfig Extension Association.
* `id` - AppConfig Extension Association ID.
* `extension_version` - The version number for the extension defined in the association.

## Import

```bash
ytofu import aws_appconfig_extension_association.example 71rxuzt
```
