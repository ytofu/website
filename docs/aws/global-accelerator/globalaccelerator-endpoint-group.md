# Globalaccelerator Endpoint Group

Manage Globalaccelerator Endpoint Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_globalaccelerator_endpoint_group:
    example:
      listener_arn: ${aws_globalaccelerator_listener.example.arn}
      endpoint_configuration:
        endpoint_id: ${aws_lb.example.arn}
        weight: 100
```
