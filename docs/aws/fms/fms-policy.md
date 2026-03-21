# FMS Policy

Manage FMS Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fms_policy:
    example:
      name: FMS-Policy-Example
      exclude_resource_tags: false
      remediation_enabled: false
      resource_type: "AWS::ElasticLoadBalancingV2::LoadBalancer"
      security_service_policy_data:
        type: WAF
        managed_service_data: '{ "type": "WAF", "ruleGroups": [{ "id": aws_wafregional_rule_group.example.id "overrideAction": { "type": "COUNT" } }] "defaultAction": { "type": "BLOCK" } "overrideCustomerWebACLAssociation": false }'
      tags:
        Name: example-fms-policy

resource:
  aws_wafregional_rule_group:
    example:
      metric_name: WAFRuleGroupExample
      name: WAF-Rule-Group-Example
```
