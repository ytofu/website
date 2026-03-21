# AppSync API Key

Create API keys for AppSync APIs using ytofu YAML.

## Basic API Key

```yaml
resource:
  aws_appsync_api_key:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      expires: 2027-01-01T00:00:00Z
```
