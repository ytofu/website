# Globalaccelerator Custom Routing Endpoint Group

Manage Globalaccelerator Custom Routing Endpoint Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_globalaccelerator_custom_routing_endpoint_group:
    example:
      listener_arn: ${aws_globalaccelerator_custom_routing_listener.example.arn}
      destination_configuration:
        from_port: 80
        to_port: 8080
        protocols: 
          - TCP
      endpoint_configuration:
        endpoint_id: ${aws_subnet.example.id}
```
