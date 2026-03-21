# API Gateway Authorizer

Configure request authorization using ytofu YAML.

## Cognito User Pool Authorizer

```yaml
resource:
  aws_api_gateway_authorizer:
    cognito:
      name: cognito
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      type: COGNITO_USER_POOLS
      provider_arns:
        - ${aws_cognito_user_pool.example.arn}
```

## Lambda Token Authorizer

```yaml
resource:
  aws_api_gateway_authorizer:
    lambda:
      name: lambda-authorizer
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      authorizer_uri: ${aws_lambda_function.authorizer.invoke_arn}
      authorizer_credentials: ${aws_iam_role.invocation_role.arn}
      type: TOKEN
      identity_source: method.request.header.Authorization
```

## Lambda Request Authorizer

```yaml
resource:
  aws_api_gateway_authorizer:
    lambda:
      name: request-authorizer
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      authorizer_uri: ${aws_lambda_function.authorizer.invoke_arn}
      authorizer_credentials: ${aws_iam_role.invocation_role.arn}
      type: REQUEST
      identity_source: method.request.header.Authorization,context.accountId
```
