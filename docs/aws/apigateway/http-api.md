# API Gateway HTTP API (v2)

Create HTTP APIs using ytofu YAML.

## Basic HTTP API

```yaml
resource:
  aws_apigatewayv2_api:
    example:
      name: example-http-api
      protocol_type: HTTP
```

## WebSocket API

```yaml
resource:
  aws_apigatewayv2_api:
    example:
      name: example-websocket-api
      protocol_type: WEBSOCKET
      route_selection_expression: $request.body.action
```

## With CORS

```yaml
resource:
  aws_apigatewayv2_api:
    example:
      name: example-http-api
      protocol_type: HTTP
      cors_configuration:
        allow_headers:
          - content-type
          - x-amz-date
          - authorization
        allow_methods:
          - GET
          - POST
          - OPTIONS
        allow_origins:
          - https://example.com
        max_age: 300
```
