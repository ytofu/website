# Apigatewayv2 Route

Manage Apigatewayv2 Route resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_api:
    example:
      name: example-websocket-api
      protocol_type: WEBSOCKET
      route_selection_expression: $request.body.action

resource:
  aws_apigatewayv2_route:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      route_key: $default
```

## HTTP Proxy Integration

```yaml
resource:
  aws_apigatewayv2_api:
    example:
      name: example-http-api
      protocol_type: HTTP

resource:
  aws_apigatewayv2_integration:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      integration_type: HTTP_PROXY
      integration_method: ANY
      integration_uri: "https://example.com/{proxy}"

resource:
  aws_apigatewayv2_route:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      route_key: "ANY /example/{proxy+}"
      target: "integrations/${aws_apigatewayv2_integration.example.id}"
```
