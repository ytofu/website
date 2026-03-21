# Connect Phone Number Contact Flow Association

Manage Connect Phone Number Contact Flow Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_phone_number_contact_flow_association:
    example:
      phone_number_id: ${aws_connect_phone_number.example.id}
      instance_id: ${aws_connect_instance.example.id}
      contact_flow_id: ${aws_connect_contact_flow.example.contact_flow_id}
```
