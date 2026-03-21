# Appsync Function

Manage Appsync Function resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example
      schema: |
        type Mutation {
        putPost(id: ID!, title: String!): Post
        }
        
        type Post {
        id: ID!
        title: String!
        }
        
        type Query {
        singlePost(id: ID!): Post
        }
        
        schema {
        query: Query
        mutation: Mutation
        }

resource:
  aws_appsync_datasource:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      name: example
      type: HTTP
      http_config:
        endpoint: "http://example.com"

resource:
  aws_appsync_function:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      data_source: ${aws_appsync_datasource.example.name}
      name: example
      request_mapping_template: |
        {
        "version": "2018-05-29",
        "method": "GET",
        "resourcePath": "/",
        "params":{
        "headers": $utils.http.copyheaders($ctx.request.headers)
        }
        }
      response_mapping_template: |
        #if($ctx.result.statusCode == 200)
        $ctx.result.body
        #else
        $utils.appendError($ctx.result.body, $ctx.result.statusCode)
        #end
```
