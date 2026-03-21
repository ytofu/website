# Servicecatalog Constraint

Manage Servicecatalog Constraint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicecatalog_constraint:
    example:
      description: "Back off, man. I'm a scientist."
      portfolio_id: ${aws_servicecatalog_portfolio.example.id}
      product_id: ${aws_servicecatalog_product.example.id}
      type: LAUNCH
      parameters: '{ "RoleArn" : "arn:aws:iam::123456789012:role/LaunchRole" }'
```
