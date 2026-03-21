# IOT Thing Principal Attachment

Manage IOT Thing Principal Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_thing:
    example:
      name: example

resource:
  aws_iot_certificate:
    cert:
      csr: file-content
      active: true

resource:
  aws_iot_thing_principal_attachment:
    att:
      principal: ${aws_iot_certificate.cert.arn}
      thing: ${aws_iot_thing.example.name}
```
