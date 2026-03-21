# AppSync Type

Define GraphQL types using ytofu YAML.

## Basic Type

```yaml
resource:
  aws_appsync_type:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      format: SDL
      definition: |
        type Mutation {
          putPost(id: ID!, title: String!): Post
        }
```
