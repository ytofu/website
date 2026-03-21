# DX Hosted Connection

Manage DX Hosted Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dx_hosted_connection:
    hosted:
      connection_id: dxcon-ffabc123
      bandwidth: 100Mbps
      name: tf-dx-hosted-connection
      owner_account_id: 123456789012
      vlan: 1
```
