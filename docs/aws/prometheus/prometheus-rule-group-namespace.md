# Resource: aws_prometheus_rule_group_namespace

Manages an Amazon Managed Service for Prometheus (AMP) Rule Group Namespace

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    demo:

  aws_prometheus_rule_group_namespace:
    demo:
      name: rules
      workspace_id: ${aws_prometheus_workspace.demo.id}
      data: |
        groups:
        - name: test
        rules:
        - record: metric:recording_rule
        expr: avg(rate(container_cpu_usage_seconds_total[5m]))```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `data` - (Required) the rule group namespace data that you want to be applied. See more [in AWS Docs](https://docs.aws.amazon.com/prometheus/latest/userguide/AMP-Ruler.html).
* `name` - (Required) The name of the rule group namespace.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `workspace_id` - (Required) ID of the prometheus workspace the rule group namespace should be linked to.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the rule group namespace.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_prometheus_rule_group_namespace.demo arn:aws:aps:us-west-2:123456789012:rulegroupsnamespace/IDstring/namespace_name
```
