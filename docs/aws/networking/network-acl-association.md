# Network Acl Association

Manage Network Acl Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_network_acl_association:
    main:
      network_acl_id: ${aws_network_acl.main.id}
      subnet_id: ${aws_subnet.main.id}
```
