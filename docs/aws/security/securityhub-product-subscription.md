# Securityhub Product Subscription

Manage Securityhub Product Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

data:
  aws_region:
    current:

resource:
  aws_securityhub_product_subscription:
    example:
      depends_on: 
        - ${aws_securityhub_account.example}
      product_arn: "arn:aws:securityhub:${data.aws_region.current.region}:733251395267:product/alertlogic/althreatmanagement"
```
