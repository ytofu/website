# Resource: aws_devicefarm_test_grid_project

Provides a resource to manage AWS Device Farm Test Grid Projects.

## Basic Example

```yaml
resource:
  aws_devicefarm_test_grid_project:
    example:
      name: example
      vpc_config:
        vpc_id: ${aws_vpc.example.id}
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: ${aws_security_group.example[*].id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the Selenium testing project.
* `description` - (Optional) Human-readable description of the project.
* `vpc_config` - (Required) The VPC security groups and subnets that are attached to a project. See [VPC Config](#vpc-config) below.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### VPC Config

* `security_group_ids` - (Required) A list of VPC security group IDs in your Amazon VPC.
* `subnet_ids` - (Required) A list of VPC subnet IDs in your Amazon VPC.
* `vpc_id` - (Required) The ID of the Amazon VPC.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name of this Test Grid Project.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_devicefarm_test_grid_project.example arn:aws:devicefarm:us-west-2:123456789012:testgrid-project:4fa784c7-ccb4-4dbf-ba4f-02198320daa1
```
