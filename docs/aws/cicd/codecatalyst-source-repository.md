# Resource: aws_codecatalyst_source_repository

ytofu resource for managing an AWS CodeCatalyst Source Repository.

## Basic Example

```yaml
resource:
  aws_codecatalyst_source_repository:
    example:
      name: example-repo
      project_name: example-project
      space_name: example-space
```

## Argument Reference

The following arguments are required:

* `name` - (Required) The name of the source repository. For more information about name requirements, see [Quotas for source repositories](https://docs.aws.amazon.com/codecatalyst/latest/userguide/source-quotas.html).
* `space_name` - (Required) The name of the CodeCatalyst space.
* `project_name` - (Required) The name of the project in the CodeCatalyst space.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) The description of the project. This description will be displayed to all users of the project. We recommend providing a brief description of the project and its intended purpose.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the source repository.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_codecatalyst_source_repository.example example-repo
```
