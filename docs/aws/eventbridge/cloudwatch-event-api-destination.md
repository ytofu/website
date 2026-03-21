# Cloudwatch Event API Destination

Manage Cloudwatch Event API Destination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_api_destination:
    test:
      name: api-destination
      description: An API Destination
      invocation_endpoint: "https://api.destination.com/endpoint"
      http_method: POST
      invocation_rate_limit_per_second: 20
      connection_arn: ${aws_cloudwatch_event_connection.test.arn}
```
