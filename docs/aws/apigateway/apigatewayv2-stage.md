# Apigatewayv2 Stage

Manage Apigatewayv2 Stage resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_stage:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      name: example-stage
```
