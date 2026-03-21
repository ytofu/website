# IOT Billing Group

Manage IOT Billing Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_billing_group:
    example:
      name: example
      properties:
        description: This is my billing group
      tags:
        terraform: true
```
