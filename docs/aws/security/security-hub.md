# Security Hub

Enable and configure AWS Security Hub using ytofu YAML.

## Enable Security Hub

```yaml
resource:
  aws_securityhub_account:
    example: {}
```

## Enable Standards

```yaml
resource:
  aws_securityhub_account:
    example: {}

  aws_securityhub_standards_subscription:
    aws_foundational:
      depends_on:
        - aws_securityhub_account.example
      standards_arn: arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0

  aws_securityhub_standards_subscription:
    pci:
      depends_on:
        - aws_securityhub_account.example
      standards_arn: arn:aws:securityhub:us-east-1::standards/pci-dss/v/3.2.1
```

## Product Integration

```yaml
resource:
  aws_securityhub_product_subscription:
    example:
      depends_on:
        - aws_securityhub_account.example
      product_arn: arn:aws:securityhub:us-east-1::product/aws/guardduty
```
