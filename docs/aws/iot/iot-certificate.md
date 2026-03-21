# IOT Certificate

Manage IOT Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_certificate:
    cert:
      csr: file-content
      active: true
```

## Without CSR

```yaml
resource:
  aws_iot_certificate:
    cert:
      active: true
```

## From existing certificate without a CA

```yaml
resource:
  aws_iot_certificate:
    cert:
      certificate_pem: file-content
      active: true
```
