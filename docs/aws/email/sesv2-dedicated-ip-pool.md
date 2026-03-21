# Sesv2 Dedicated IP Pool

Manage Sesv2 Dedicated IP Pool resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sesv2_dedicated_ip_pool:
    example:
      pool_name: my-pool
```

## Managed Pool

```yaml
resource:
  aws_sesv2_dedicated_ip_pool:
    example:
      pool_name: my-managed-pool
      scaling_mode: MANAGED
```
