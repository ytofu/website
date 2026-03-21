# Resource: aws_resourcegroups_resource

ytofu resource for managing an AWS Resource Groups Resource.

## Basic Example

```yaml
resource:
  aws_ec2_host:
    example:
      instance_family: t3
      availability_zone: us-east-1a
      host_recovery: off
      auto_placement: on

  aws_resourcegroups_group:
    example:
      name: example

  aws_resourcegroups_resource:
    example:
      group_arn: ${aws_resourcegroups_group.example.arn}
      resource_arn: ${aws_ec2_host.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `group_arn` - (Required) Name or ARN of the resource group to add resources to.
* `resource_arn` - (Required) ARN of the resource to be added to the group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A comma-delimited string combining `group_arn` and `resource_arn`.
* `resource_type` - The resource type of a resource, such as `AWS::EC2::Instance`.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_resourcegroups_resource.example arn:aws:resource-groups:us-west-2:012345678901:group/example,arn:aws:lambda:us-west-2:012345678901:function:example
```
