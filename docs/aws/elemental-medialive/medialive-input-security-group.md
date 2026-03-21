# Medialive Input Security Group

Manage Medialive Input Security Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_medialive_input_security_group:
    example:
      whitelist_rules:
        cidr: 10.0.0.8/32
      tags:
        ENVIRONMENT: prod
```
