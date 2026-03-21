# Networkfirewall Resource Policy

Manage Networkfirewall Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkfirewall_resource_policy:
    example:
      resource_arn: ${aws_networkfirewall_firewall_policy.example.arn}
      policy: '{ "Statement": [{ "Action": [ "network-firewall:ListFirewallPolicies", "network-firewall:CreateFirewall", "network-firewall:UpdateFirewall", "network-firewall:AssociateFirewallPolicy" ] "Effect": "Allow" "Resource": aws_networkfirewall_firewall_policy.example.arn "Principal": { "AWS": "arn:aws:iam::123456789012:root" } }] "Version": "2012-10-17" }'
```

## For a Rule Group resource

```yaml
resource:
  aws_networkfirewall_resource_policy:
    example:
      resource_arn: ${aws_networkfirewall_rule_group.example.arn}
      policy: '{ "Statement": [{ "Action": [ "network-firewall:ListRuleGroups", "network-firewall:CreateFirewallPolicy", "network-firewall:UpdateFirewallPolicy" ] "Effect": "Allow" "Resource": aws_networkfirewall_rule_group.example.arn "Principal": { "AWS": "arn:aws:iam::123456789012:root" } }] "Version": "2012-10-17" }'
```
