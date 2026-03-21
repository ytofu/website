# Appsync Type

Manage Appsync Type resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example

resource:
  aws_appsync_type:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      format: SDL
      definition: |
        type Mutation
        
        {
        putPost(id: ID!,title: String! ): Post
        
        }
```
