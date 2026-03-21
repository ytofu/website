# Network Interface Permission

Manage Network Interface Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_network_interface:
    example:
      subnet_id: ${aws_subnet.example.id}
      private_ips: 
        - 10.0.0.50
      security_groups: 
        - ${aws_security_group.example.id}
      attachment:
        instance: ${aws_instance.example.id}
        device_index: 1

resource:
  aws_network_interface_permission:
    example:
      network_interface_id: ${aws_network_interface.example.id}
      aws_account_id: 123456789012
      permission: INSTANCE-ATTACH
```
