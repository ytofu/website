# Resource: aws_codecatalyst_project

ytofu resource for managing an AWS CodeCatalyst Project.

## Basic Example

```yaml
resource:
  aws_codecatalyst_project:
    test:
      space_name: myproject
      display_name: MyProject
      description: My CodeCatalyst Project created using Terraform
```

## Argument Reference

The following arguments are required:

* `space_name` - (Required) The name of the space.
* `display_name` - (Required) The friendly name of the project that will be displayed to users.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) The description of the project. This description will be displayed to all users of the project. We recommend providing a brief description of the project and its intended purpose.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the project in the space.
* `name` - The name of the project in the space.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_codecatalyst_project.example project-id-12345678
```
