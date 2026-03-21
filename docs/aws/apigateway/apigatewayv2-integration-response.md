# Apigatewayv2 Integration Response

Manage Apigatewayv2 Integration Response resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_integration_response:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      integration_id: ${aws_apigatewayv2_integration.example.id}
      integration_response_key: /200/
```
