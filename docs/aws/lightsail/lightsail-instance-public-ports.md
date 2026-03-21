# Lightsail Instance Public Ports

Manage Lightsail Instance Public Ports resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_lightsail_instance:
    example:
      name: example-instance
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0

resource:
  aws_lightsail_instance_public_ports:
    example:
      instance_name: ${aws_lightsail_instance.example.name}
      port_info:
        protocol: tcp
        from_port: 80
        to_port: 80
      port_info:
        protocol: tcp
        from_port: 443
        to_port: 443
        cidrs: 
          - 192.168.1.0/24
```
