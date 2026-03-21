# Networkfirewall Firewall Policy

Manage Networkfirewall Firewall Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

data:
  aws_partition:
    current:

data:
  aws_caller_identity:
    current:

resource:
  aws_networkfirewall_firewall_policy:
    example:
      name: example
      firewall_policy:
        stateless_default_actions: 
          - "aws:pass"
        stateless_fragment_default_actions: 
          - "aws:drop"
        stateless_rule_group_reference:
          priority: 1
          resource_arn: ${aws_networkfirewall_rule_group.example.arn}
        tls_inspection_configuration_arn: "arn:${data.aws_partition.current.partition}:network-firewall:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:tls-configuration/example"
      tags:
        Tag1: Value1
        Tag2: Value2
```
