# DX Lag

Manage DX Lag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dx_lag:
    hoge:
      name: tf-dx-lag
      connections_bandwidth: 1Gbps
      location: EqDC2
      force_destroy: true
```
