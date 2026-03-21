# Resource: aws_appconfig_application

Provides an AppConfig Application resource.

## Basic Example

```yaml
resource:
  aws_appconfig_application:
    example:
      name: example-application-tf
      description: Example AppConfig Application
      tags:
        Type: AppConfig Application
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name for the application. Must be between 1 and 64 characters in length.
* `description` - (Optional) Description of the application. Can be at most 1024 characters.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the AppConfig Application.
* `id` - AppConfig application ID.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_appconfig_application.example 71rxuzt
```
