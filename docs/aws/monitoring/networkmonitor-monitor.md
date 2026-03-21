# Resource: aws_networkmonitor_monitor

ytofu resource for managing an AWS Network Monitor Monitor.

## Basic Example

```yaml
resource:
  aws_networkmonitor_monitor:
    example:
      aggregation_period: 30
      monitor_name: example
```

## Argument Reference

The following arguments are required:

- `monitor_name` - (Required) The name of the monitor.

The following arguments are optional:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `aggregation_period` - (Optional) The time, in seconds, that metrics are aggregated and sent to Amazon CloudWatch. Valid values are either 30 or 60.
- `tags` - (Optional) Key-value tags for the monitor. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `arn` - The ARN of the monitor.
- `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_networkmonitor_monitor.example monitor-7786087912324693644
```
