# Network Interface Attachment

Manage Network Interface Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_network_interface_attachment:
    test:
      instance_id: ${aws_instance.test.id}
      network_interface_id: ${aws_network_interface.test.id}
      device_index: 0
```
