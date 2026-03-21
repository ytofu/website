# Resource: aws_elasticache_parameter_group

Provides an ElastiCache parameter group resource.

## Basic Example

```yaml
resource:
  aws_elasticache_parameter_group:
    default:
      name: cache-params
      family: redis2.8
      parameter:
        name: activerehashing
        value: yes
      parameter:
        name: min-slaves-to-write
        value: 2
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the ElastiCache parameter group.
* `family` - (Required) The family of the ElastiCache parameter group.
* `description` - (Optional) The description of the ElastiCache parameter group. Defaults to "Managed by ytofu".
* `parameter` - (Optional) A list of ElastiCache parameters to apply.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

Parameter blocks support the following:

* `name` - (Required) The name of the ElastiCache parameter.
* `value` - (Required) The value of the ElastiCache parameter.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ElastiCache parameter group name.
* `arn` - The AWS ARN associated with the parameter group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_elasticache_parameter_group.default redis-params
```
