# DMS Certificate

Manage DMS Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dms_certificate:
    test:
      certificate_id: test-dms-certificate-tf
      certificate_pem: ...
      tags:
        Name: test
```
