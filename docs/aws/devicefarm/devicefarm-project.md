# Resource: aws_devicefarm_project

Provides a resource to manage AWS Device Farm Projects.

## Basic Example

```yaml
resource:
  aws_devicefarm_project:
    awesome_devices:
      name: my-device-farm
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the project
* `default_job_timeout_minutes` - (Optional) Sets the execution timeout value (in minutes) for a project. All test runs in this project use the specified execution timeout value unless overridden when scheduling a run.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name of this project
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

[aws-get-project]: http://docs.aws.amazon.com/devicefarm/latest/APIReference/API_GetProject.html

## Import

```bash
ytofu import aws_devicefarm_project.example arn:aws:devicefarm:us-west-2:123456789012:project:4fa784c7-ccb4-4dbf-ba4f-02198320daa1
```
