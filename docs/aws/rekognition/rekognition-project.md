# Resource: aws_rekognition_project

ytofu resource for managing an AWS Rekognition Project.

## Basic Example

```yaml
resource:
  aws_rekognition_project:
    example:
      name: example-project
      auto_update: ENABLED
      feature: CONTENT_MODERATION
```

## Custom Labels

```yaml
resource:
  aws_rekognition_project:
    example:
      name: example-project
      feature: CUSTOM_LABELS
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Desired name of the project.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `auto_update` - (Optional) Specify if automatic retraining should occur. Valid values are `ENABLED` or `DISABLED`. Must be set when `feature` is `CONTENT_MODERATION`, but do not set otherwise.
* `feature` - (Optional) Specify the feature being customized. Valid values are `CONTENT_MODERATION` or `CUSTOM_LABELS`. Defaults to `CUSTOM_LABELS`.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Project.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_rekognition_project.example project-id-12345678
```
