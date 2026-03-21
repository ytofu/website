# AppSync Resolver

Create field resolvers for AppSync APIs using ytofu YAML.

## Unit Resolver

```yaml
resource:
  aws_appsync_resolver:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      field: getPost
      type: Query
      data_source: ${aws_appsync_datasource.example.name}
      request_template: |
        {
          "version": "2017-02-28",
          "operation": "GetItem",
          "key": {
            "id": $util.dynamodb.toDynamoDBJson($ctx.args.id)
          }
        }
      response_template: $util.toJson($ctx.result)
```

## Pipeline Resolver

```yaml
resource:
  aws_appsync_resolver:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      field: createPost
      type: Mutation
      kind: PIPELINE
      pipeline_config:
        functions:
          - ${aws_appsync_function.validate.function_id}
          - ${aws_appsync_function.save.function_id}
      request_template: "{}"
      response_template: $util.toJson($ctx.result)
```

## JS Resolver

```yaml
resource:
  aws_appsync_resolver:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      type: Query
      field: getPost
      data_source: ${aws_appsync_datasource.example.name}
      runtime:
        name: APPSYNC_JS
        runtime_version: 1.0.0
      code: |
        export function request(ctx) {
          return {
            operation: 'GetItem',
            key: util.dynamodb.toMapValues({id: ctx.args.id}),
          };
        }
        export function response(ctx) {
          return ctx.result;
        }
```
