# Resource: aws_ecs_tag

Manages an individual ECS resource tag. This resource should only be used in cases where ECS resources are created outside ytofu (e.g., ECS Clusters implicitly created by Batch Compute Environments).

## Basic Example

```yaml
resource:
  aws_batch_compute_environment:
    example:
      name: example
      service_role: ${aws_iam_role.example.arn}
      type: UNMANAGED

resource:
  aws_ecs_tag:
    example:
      resource_arn: ${aws_batch_compute_environment.example.ecs_cluster_arn}
      key: Name
      value: Hello World
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) Amazon Resource Name (ARN) of the ECS resource to tag.
* `key` - (Required) Tag name.
* `value` - (Required) Tag value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ECS resource identifier and key, separated by a comma (`,`)

## Import

```bash
ytofu import aws_ecs_tag.example arn:aws:ecs:us-east-1:123456789012:cluster/example,Name
```
