# Resource: aws_networkfirewall_resource_policy

Provides an AWS Network Firewall Resource Policy Resource for a rule group or firewall policy.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy` - (Required) JSON formatted policy document that controls access to the Network Firewall resource. The policy must be provided **without whitespaces**.  We recommend using jsonencode for formatting as seen in the examples above. For more details, including available policy statement Actions, see the [Policy](https://docs.aws.amazon.com/network-firewall/latest/APIReference/API_PutResourcePolicy.html#API_PutResourcePolicy_RequestSyntax) parameter in the AWS API documentation.
* `resource_arn` - (Required, Forces new resource) The Amazon Resource Name (ARN) of the rule group or firewall policy.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Resource Name (ARN) of the rule group or firewall policy associated with the resource policy.

## Import

```bash
ytofu import aws_networkfirewall_resource_policy.example aws_networkfirewall_rule_group.example arn:aws:network-firewall:us-west-1:123456789012:stateful-rulegroup/example
```
