# Resource: aws_waf_rule

Provides a WAF Rule Resource

## Basic Example

```yaml
resource:
  aws_waf_ipset:
    ipset:
      name: tfIPSet
      ip_set_descriptors:
        type: IPV4
        value: 192.0.7.0/24

  aws_waf_rule:
    wafrule:
      depends_on: 
        - ${aws_waf_ipset.ipset}
      name: tfWAFRule
      metric_name: tfWAFRule
      predicates:
        data_id: ${aws_waf_ipset.ipset.id}
        negated: false
        type: IPMatch```

## Argument Reference

This resource supports the following arguments:

* `metric_name` - (Required) The name or description for the Amazon CloudWatch metric of this rule. The name can contain only alphanumeric characters (A-Z, a-z, 0-9); the name can't contain whitespace.
* `name` - (Required) The name or description of the rule.
* `predicates` - (Optional) The objects to include in a rule (documented below).
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF rule.
* `arn` - The ARN of the WAF rule.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_waf_rule.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
