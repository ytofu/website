# Resource: aws_scheduler_schedule_group

Provides an EventBridge Scheduler Schedule Group resource.

## Basic Example

```yaml
resource:
  aws_scheduler_schedule_group:
    example:
      name: my-schedule-group
```

## Argument Reference

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) Name of the schedule group. If omitted, ytofu will assign a random, unique name. Conflicts with `name_prefix`.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Name of the schedule group.
* `arn` - ARN of the schedule group.
* `creation_date` - Time at which the schedule group was created.
* `last_modification_date` - Time at which the schedule group was last modified.
* `state` - State of the schedule group. Can be `ACTIVE` or `DELETING`.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_scheduler_schedule_group.example my-schedule-group
```
