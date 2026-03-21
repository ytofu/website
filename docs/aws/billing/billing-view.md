# Billing View

Manage Billing View resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_billing_view:
    example:
      name: example
      description: example description
      source_views: 
        - "arn:aws:billing::123456789012:billingview/example"
```
