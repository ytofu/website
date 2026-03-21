# Appsync Channel Namespace

Manage Appsync Channel Namespace resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_channel_namespace:
    example:
      name: example-channel-namespace
      api_id: ${aws_appsync_api.example.api_id}
```
