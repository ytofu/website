# Connect Quick Connect

Manage Connect Quick Connect resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_quick_connect:
    test:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Example Name
      description: quick connect phone number
      quick_connect_config:
        quick_connect_type: PHONE_NUMBER
        phone_config:
          phone_number: +12345678912
      tags: 
```
