# DB Snapshot Copy

Manage DB Snapshot Copy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_db_instance:
    example:
      allocated_storage: 10
      engine: mysql
      engine_version: 5.6.21
      instance_class: db.t2.micro
      db_name: baz
      password: barbarbarbar
      username: foo
      maintenance_window: "Fri:09:00-Fri:09:30"
      backup_retention_period: 0
      parameter_group_name: default.mysql5.6

resource:
  aws_db_snapshot:
    example:
      db_instance_identifier: ${aws_db_instance.example.identifier}
      db_snapshot_identifier: testsnapshot1234

resource:
  aws_db_snapshot_copy:
    example:
      source_db_snapshot_identifier: ${aws_db_snapshot.example.db_snapshot_arn}
      target_db_snapshot_identifier: testsnapshot1234-copy
```
