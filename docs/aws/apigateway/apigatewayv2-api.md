# Apigatewayv2 API

Manage Apigatewayv2 API resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_api:
    example:
      name: example-websocket-api
      protocol_type: WEBSOCKET
      route_selection_expression: $request.body.action
```

## Basic HTTP API

```yaml
resource:
  aws_apigatewayv2_api:
    example:
      name: example-http-api
      protocol_type: HTTP
```
