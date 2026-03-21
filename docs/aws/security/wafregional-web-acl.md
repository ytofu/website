# Wafregional Web Acl

Manage Wafregional Web Acl resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_wafregional_ipset:
    ipset:
      name: tfIPSet
      ip_set_descriptor:
        type: IPV4
        value: 192.0.7.0/24

resource:
  aws_wafregional_rule:
    wafrule:
      name: tfWAFRule
      metric_name: tfWAFRule
      predicate:
        data_id: ${aws_wafregional_ipset.ipset.id}
        negated: false
        type: IPMatch

resource:
  aws_wafregional_web_acl:
    wafacl:
      name: tfWebACL
      metric_name: tfWebACL
      default_action:
        type: ALLOW
      rule:
        action:
          type: BLOCK
        priority: 1
        rule_id: ${aws_wafregional_rule.wafrule.id}
        type: REGULAR
```

## Group Rule

```yaml
resource:
  aws_wafregional_web_acl:
    example:
      name: example
      metric_name: example
      default_action:
        type: ALLOW
      rule:
        priority: 1
        rule_id: ${aws_wafregional_rule_group.example.id}
        type: GROUP
        override_action:
          type: NONE
```

## Logging

```yaml
resource:
  aws_wafregional_web_acl:
    example:
      logging_configuration:
        log_destination: ${aws_kinesis_firehose_delivery_stream.example.arn}
        redacted_fields:
          field_to_match:
            type: URI
          field_to_match:
            data: referer
            type: HEADER
```
