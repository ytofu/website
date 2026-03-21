# DMS Certificate

Import SSL certificates for DMS endpoints using ytofu YAML.

## Basic Certificate

```yaml
resource:
  aws_dms_certificate:
    example:
      certificate_id: example
      certificate_pem: file-content
```
