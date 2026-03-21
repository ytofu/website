# Apigatewayv2 Authorizer

Manage Apigatewayv2 Authorizer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_authorizer:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      authorizer_type: REQUEST
      authorizer_uri: ${aws_lambda_function.example.invoke_arn}
      identity_sources: 
        - route.request.header.Auth
      name: example-authorizer
```

## Basic HTTP API

```yaml
resource:
  aws_apigatewayv2_authorizer:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      authorizer_type: REQUEST
      authorizer_uri: ${aws_lambda_function.example.invoke_arn}
      identity_sources: 
        - $request.header.Authorization
      name: example-authorizer
      authorizer_payload_format_version: 2.0
```
