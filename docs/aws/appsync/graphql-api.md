# AppSync GraphQL API

Create GraphQL APIs using ytofu YAML.

## API Key Auth

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example
```

## Cognito Auth

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: AMAZON_COGNITO_USER_POOLS
      name: example
      user_pool_config:
        aws_region: ${data.aws_region.current.name}
        default_action: ALLOW
        user_pool_id: ${aws_cognito_user_pool.example.id}
```

## IAM Auth with Schema

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: AWS_IAM
      name: example
      schema: |
        type Query {
          getPost(id: ID!): Post
        }
        type Post {
          id: ID!
          title: String
          content: String
        }
```

## With Logging

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example
      log_config:
        cloudwatch_logs_role_arn: ${aws_iam_role.example.arn}
        field_log_level: ERROR
```
