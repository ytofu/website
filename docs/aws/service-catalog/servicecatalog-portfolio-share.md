# Servicecatalog Portfolio Share

Manage Servicecatalog Portfolio Share resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicecatalog_portfolio_share:
    example:
      principal_id: 012128675309
      portfolio_id: ${aws_servicecatalog_portfolio.example.id}
      type: ACCOUNT
```
