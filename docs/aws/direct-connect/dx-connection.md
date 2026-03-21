# DX Connection

Manage DX Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dx_connection:
    hoge:
      name: tf-dx-connection
      bandwidth: 1Gbps
      location: EqDC2
```

## Request a MACsec-capable connection

```yaml
resource:
  aws_dx_connection:
    example:
      name: tf-dx-connection
      bandwidth: 10Gbps
      location: EqDA2
      request_macsec: true
```

## Configure encryption mode for MACsec-capable connections

```yaml
resource:
  aws_dx_connection:
    example:
      name: tf-dx-connection
      bandwidth: 10Gbps
      location: EqDC2
      request_macsec: true
      encryption_mode: must_encrypt
```
