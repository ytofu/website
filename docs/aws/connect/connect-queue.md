# Connect Queue

Manage Connect Queue resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_queue:
    test:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Example Name
      description: Example Description
      hours_of_operation_id: 12345678-1234-1234-1234-123456789012
      tags: 
```

## With Quick Connect IDs

```yaml
resource:
  aws_connect_queue:
    test:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Example Name
      description: Example Description
      hours_of_operation_id: 12345678-1234-1234-1234-123456789012
      quick_connect_ids:
        - 12345678-abcd-1234-abcd-123456789012
      tags: 
```

## With Outbound Caller Config

```yaml
resource:
  aws_connect_queue:
    test:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Example Name
      description: Example Description
      hours_of_operation_id: 12345678-1234-1234-1234-123456789012
      outbound_caller_config:
        outbound_caller_id_name: example
        outbound_caller_id_number_id: 12345678-abcd-1234-abcd-123456789012
        outbound_flow_id: 87654321-defg-1234-defg-987654321234
      tags: 
```
