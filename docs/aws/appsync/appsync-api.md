# Appsync API

Manage Appsync API resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_api:
    example:
      name: example-event-api
      event_config:
        auth_provider:
          auth_type: API_KEY
        connection_auth_mode:
          auth_type: API_KEY
        default_publish_auth_mode:
          auth_type: API_KEY
        default_subscribe_auth_mode:
          auth_type: API_KEY
```

## With Cognito Authentication

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example-user-pool

resource:
  aws_appsync_api:
    example:
      name: example-event-api
      event_config:
        auth_provider:
          auth_type: AMAZON_COGNITO_USER_POOLS
          cognito_config:
            user_pool_id: ${aws_cognito_user_pool.example.id}
            aws_region: ${data.aws_region.current.name}
        connection_auth_mode:
          auth_type: AMAZON_COGNITO_USER_POOLS
        default_publish_auth_mode:
          auth_type: AMAZON_COGNITO_USER_POOLS
        default_subscribe_auth_mode:
          auth_type: AMAZON_COGNITO_USER_POOLS

data:
  aws_region:
    current:
```

## With Lambda Authorizer

```yaml
resource:
  aws_appsync_api:
    example:
      name: example-event-api
      event_config:
        auth_provider:
          auth_type: AWS_LAMBDA
          lambda_authorizer_config:
            authorizer_uri: ${aws_lambda_function.example.arn}
            authorizer_result_ttl_in_seconds: 300
        connection_auth_mode:
          auth_type: AWS_LAMBDA
        default_publish_auth_mode:
          auth_type: AWS_LAMBDA
        default_subscribe_auth_mode:
          auth_type: AWS_LAMBDA
```
