# Resource: aws_wafregional_rule_group

Provides a WAF Regional Rule Group Resource

## Basic Example

```yaml
resource:
  aws_wafregional_rule:
    example:
      name: example
      metric_name: example

  aws_wafregional_rule_group:
    example:
      name: example
      metric_name: example
      activated_rule:
        action:
          type: COUNT
        priority: 50
        rule_id: ${aws_wafregional_rule.example.id}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A friendly name of the rule group
* `metric_name` - (Required) A friendly name for the metrics from the rule group
* `activated_rule` - (Optional) A list of activated rules, see below
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF Regional Rule Group.
* `arn` - The ARN of the WAF Regional Rule Group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_wafregional_rule_group.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
