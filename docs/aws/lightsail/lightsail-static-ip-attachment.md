# Lightsail Static IP Attachment

Manage Lightsail Static IP Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_static_ip:
    example:
      name: example

resource:
  aws_lightsail_instance:
    example:
      name: example
      availability_zone: us-east-1a
      blueprint_id: ubuntu_20_04
      bundle_id: nano_2_0

resource:
  aws_lightsail_static_ip_attachment:
    example:
      static_ip_name: ${aws_lightsail_static_ip.example.name}
      instance_name: ${aws_lightsail_instance.example.name}
```
