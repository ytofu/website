# Resource: aws_amplify_backend_environment

Provides an Amplify Backend Environment resource.

## Basic Example

```yaml
resource:
  aws_amplify_app:
    example:
      name: example

  aws_amplify_backend_environment:
    example:
      app_id: ${aws_amplify_app.example.id}
      environment_name: example
      deployment_artifacts: app-example-deployment
      stack_name: amplify-app-example```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `app_id` - (Required) Unique ID for an Amplify app.
* `environment_name` - (Required) Name for the backend environment.
* `deployment_artifacts` - (Optional) Name of deployment artifacts.
* `stack_name` - (Optional) AWS CloudFormation stack name of a backend environment.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN for a backend environment that is part of an Amplify app.
* `id` - Unique ID of the Amplify backend environment.

## Import

```bash
ytofu import aws_amplify_backend_environment.example d2ypk4k47z8u6/example
```
