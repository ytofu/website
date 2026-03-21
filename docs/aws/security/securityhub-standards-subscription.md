# Securityhub Standards Subscription

Manage Securityhub Standards Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

data:
  aws_region:
    current:

resource:
  aws_securityhub_standards_subscription:
    cis:
      depends_on: 
        - ${aws_securityhub_account.example}
      standards_arn: "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0"

resource:
  aws_securityhub_standards_subscription:
    pci_321:
      depends_on: 
        - ${aws_securityhub_account.example}
      standards_arn: "arn:aws:securityhub:${data.aws_region.current.region}::standards/pci-dss/v/3.2.1"
```
