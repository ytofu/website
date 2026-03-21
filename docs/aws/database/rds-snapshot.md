# RDS Snapshot

Create database snapshots using ytofu YAML.

## Basic Snapshot

```yaml
resource:
  aws_db_snapshot:
    test:
      db_instance_identifier: ${aws_db_instance.bar.identifier}
      db_snapshot_identifier: testsnapshot1234
```

## With Tags

```yaml
resource:
  aws_db_snapshot:
    production:
      db_instance_identifier: ${aws_db_instance.production.identifier}
      db_snapshot_identifier: production-snapshot
      tags:
        Name: Production Snapshot
        Environment: production
```
