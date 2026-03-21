# Connect Instance

Manage Connect Instance resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_instance:
    test:
      identity_management_type: CONNECT_MANAGED
      inbound_calls_enabled: true
      instance_alias: friendly-name-connect
      outbound_calls_enabled: true
      tags: 
```
