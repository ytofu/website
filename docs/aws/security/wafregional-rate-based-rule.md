# Wafregional Rate Based Rule

Manage Wafregional Rate Based Rule resources using ytofu YAML.

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
  aws_wafregional_rate_based_rule:
    wafrule:
      depends_on: 
        - ${aws_wafregional_ipset.ipset}
      name: tfWAFRule
      metric_name: tfWAFRule
      rate_key: IP
      rate_limit: 100
      predicate:
        data_id: ${aws_wafregional_ipset.ipset.id}
        negated: false
        type: IPMatch
```
