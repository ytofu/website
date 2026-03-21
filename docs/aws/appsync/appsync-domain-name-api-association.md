# Appsync Domain Name API Association

Manage Appsync Domain Name API Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_domain_name_api_association:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      domain_name: ${aws_appsync_domain_name.example.domain_name}
```
