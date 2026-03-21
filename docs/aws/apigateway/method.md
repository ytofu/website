# API Gateway Method

Define HTTP methods on API resources using ytofu YAML.

## Basic Method (No Auth)

```yaml
resource:
  aws_api_gateway_method:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: GET
      authorization: NONE
```

## With Cognito Authorizer

```yaml
resource:
  aws_api_gateway_authorizer:
    cognito:
      name: cognito-authorizer
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      type: COGNITO_USER_POOLS
      provider_arns:
        - ${aws_cognito_user_pool.example.arn}

  aws_api_gateway_method:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: GET
      authorization: COGNITO_USER_POOLS
      authorizer_id: ${aws_api_gateway_authorizer.cognito.id}
```

## With API Key Required

```yaml
resource:
  aws_api_gateway_method:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: POST
      authorization: NONE
      api_key_required: true
```

## Method Response

```yaml
resource:
  aws_api_gateway_method_response:
    ok:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      resource_id: ${aws_api_gateway_resource.example.id}
      http_method: ${aws_api_gateway_method.example.http_method}
      status_code: "200"
      response_models:
        application/json: Empty
```
