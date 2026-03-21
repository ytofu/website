# Cloudwatch Event Connection

Manage Cloudwatch Event Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_connection:
    test:
      name: ngrok-connection
      description: A connection description
      authorization_type: API_KEY
      auth_parameters:
        api_key:
          key: x-signature
          value: 1234
```
