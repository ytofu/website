# Lightsail Domain Entry

Manage Lightsail Domain Entry resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_domain:
    example:
      domain_name: example.com

resource:
  aws_lightsail_domain_entry:
    example:
      domain_name: ${aws_lightsail_domain.example.domain_name}
      name: www
      type: A
      target: 127.0.0.1
```
