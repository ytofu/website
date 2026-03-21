# AppSync Function

Create pipeline functions for AppSync APIs using ytofu YAML.

## Basic Function

```yaml
resource:
  aws_appsync_function:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      data_source: ${aws_appsync_datasource.example.name}
      name: example
      request_mapping_template: |
        {
          "version": "2018-05-29",
          "operation": "GetItem",
          "key": {
            "id": $util.dynamodb.toDynamoDBJson($ctx.stash.id)
          }
        }
      response_mapping_template: $util.toJson($ctx.result)
```
