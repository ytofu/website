# AppSync DataSource

Configure data sources for AppSync APIs using ytofu YAML.

## DynamoDB Data Source

```yaml
resource:
  aws_appsync_datasource:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      name: example
      service_role_arn: ${aws_iam_role.example.arn}
      type: AMAZON_DYNAMODB
      dynamodb_config:
        table_name: ${aws_dynamodb_table.example.name}
```

## Lambda Data Source

```yaml
resource:
  aws_appsync_datasource:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      name: example
      service_role_arn: ${aws_iam_role.example.arn}
      type: AWS_LAMBDA
      lambda_config:
        function_arn: ${aws_lambda_function.example.arn}
```

## HTTP Data Source

```yaml
resource:
  aws_appsync_datasource:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      name: example
      type: HTTP
      http_config:
        endpoint: https://api.example.com
```

## None Data Source

```yaml
resource:
  aws_appsync_datasource:
    none:
      api_id: ${aws_appsync_graphql_api.example.id}
      name: none
      type: NONE
```
