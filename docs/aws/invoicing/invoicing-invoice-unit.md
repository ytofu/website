# Invoicing Invoice Unit

Manage Invoicing Invoice Unit resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_invoicing_invoice_unit:
    example:
      name: example-unit
      description: Example invoice unit
      invoice_receiver: 123456789012
      rule:
        linked_accounts: 
          - 098765432109
      tags:
        Environment: production
```
