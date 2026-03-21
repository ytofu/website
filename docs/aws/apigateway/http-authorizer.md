# API Gateway v2 Authorizer

Configure authorization for HTTP APIs using ytofu YAML.

## JWT Authorizer

```yaml
resource:
  aws_apigatewayv2_authorizer:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      authorizer_type: JWT
      identity_sources:
        - $request.header.Authorization
      name: example
      jwt_configuration:
        audience:
          - ${aws_cognito_user_pool_client.example.id}
        issuer: https://${aws_cognito_user_pool.example.endpoint}
```

## Lambda Authorizer

```yaml
resource:
  aws_apigatewayv2_authorizer:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      authorizer_type: REQUEST
      authorizer_uri: ${aws_lambda_function.authorizer.invoke_arn}
      authorizer_payload_format_version: "2.0"
      name: lambda-authorizer
      enable_simple_responses: true
```
