# Medialive Input

Manage Medialive Input resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_medialive_input_security_group:
    example:
      whitelist_rules:
        cidr: 10.0.0.8/32
      tags:
        ENVIRONMENT: prod

resource:
  aws_medialive_input:
    example:
      name: example-input
      input_security_groups: 
        - ${aws_medialive_input_security_group.example.id}
      type: UDP_PUSH
      tags:
        ENVIRONMENT: prod
```
