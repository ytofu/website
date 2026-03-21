# Appsync API Cache

Manage Appsync API Cache resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example

resource:
  aws_appsync_api_cache:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      api_caching_behavior: FULL_REQUEST_CACHING
      type: LARGE
      ttl: 900
```
