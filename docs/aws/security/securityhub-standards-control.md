# Securityhub Standards Control

Manage Securityhub Standards Control resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_standards_subscription:
    cis_aws_foundations_benchmark:
      standards_arn: "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0"
      depends_on: 
        - ${aws_securityhub_account.example}

resource:
  aws_securityhub_standards_control:
    ensure_iam_password_policy_prevents_password_reuse:
      standards_control_arn: "arn:aws:securityhub:us-east-1:111111111111:control/cis-aws-foundations-benchmark/v/1.2.0/1.10"
      control_status: DISABLED
      disabled_reason: We handle password policies within Okta
      depends_on: 
        - ${aws_securityhub_standards_subscription.cis_aws_foundations_benchmark}
```
