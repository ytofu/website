# Globalaccelerator Custom Routing Listener

Manage Globalaccelerator Custom Routing Listener resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_globalaccelerator_custom_routing_accelerator:
    example:
      name: Example
      ip_address_type: IPV4
      enabled: true
      attributes:
        flow_logs_enabled: true
        flow_logs_s3_bucket: example-bucket
        flow_logs_s3_prefix: flow-logs/

resource:
  aws_globalaccelerator_custom_routing_listener:
    example:
      accelerator_arn: ${aws_globalaccelerator_custom_routing_accelerator.example.arn}
      port_range:
        from_port: 80
        to_port: 80
```
