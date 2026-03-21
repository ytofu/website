# API Gateway v2 Route

Create routes for HTTP APIs using ytofu YAML.

## Basic Route

```yaml
resource:
  aws_apigatewayv2_route:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      route_key: GET /hello
      target: integrations/${aws_apigatewayv2_integration.example.id}
```

## With Authorizer

```yaml
resource:
  aws_apigatewayv2_route:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      route_key: GET /protected
      target: integrations/${aws_apigatewayv2_integration.example.id}
      authorization_type: JWT
      authorizer_id: ${aws_apigatewayv2_authorizer.example.id}
```

## $default Route

```yaml
resource:
  aws_apigatewayv2_route:
    default:
      api_id: ${aws_apigatewayv2_api.example.id}
      route_key: $default
      target: integrations/${aws_apigatewayv2_integration.example.id}
```
