# Securityhub Standards Control Association

Manage Securityhub Standards Control Association resources using ytofu YAML.

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
  aws_securityhub_standards_control_association:
    cis_aws_foundations_benchmark_disable_iam_1:
      standards_arn: ${aws_securityhub_standards_subscription.cis_aws_foundations_benchmark.standards_arn}
      security_control_id: IAM.1
      association_status: DISABLED
      updated_reason: Not needed
```
