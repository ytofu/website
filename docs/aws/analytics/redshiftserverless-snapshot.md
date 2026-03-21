# Redshiftserverless Snapshot

Manage Redshiftserverless Snapshot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshiftserverless_snapshot:
    example:
      namespace_name: ${aws_redshiftserverless_workgroup.example.namespace_name}
      snapshot_name: example
```
