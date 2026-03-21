# Lightsail Certificate

Manage Lightsail Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_certificate:
    example:
      name: example-certificate
      domain_name: example.com
      subject_alternative_names: 
        - www.example.com
```
