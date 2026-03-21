# IOT Domain Configuration

Manage IOT Domain Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_domain_configuration:
    iot:
      name: iot-
      domain_name: iot.example.com
      service_type: DATA
      server_certificate_arns:
        - ${aws_acm_certificate.cert.arn}
```
