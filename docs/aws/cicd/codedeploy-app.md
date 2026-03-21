# Resource: aws_codedeploy_app

Provides a CodeDeploy application to be used as a basis for deployments

## Basic Example

```yaml
resource:
  aws_codedeploy_app:
    example:
      compute_platform: ECS
      name: example
```

## Lambda Application

```yaml
resource:
  aws_codedeploy_app:
    example:
      compute_platform: Lambda
      name: example
```

## Server Application

```yaml
resource:
  aws_codedeploy_app:
    example:
      compute_platform: Server
      name: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the application.
* `compute_platform` - (Optional) The compute platform can either be `ECS`, `Lambda`, or `Server`. Default is `Server`.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the CodeDeploy application.
* `application_id` - The application ID.
* `id` - Amazon's assigned ID for the application.
* `name` - The application's name.
* `github_account_name` - The name for a connection to a GitHub account.
* `linked_to_github` - Whether the user has authenticated with GitHub for the specified application.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_codedeploy_app.example my-application
```
