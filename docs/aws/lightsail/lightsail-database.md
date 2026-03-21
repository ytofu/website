# Lightsail Database

Manage Lightsail Database resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_database:
    example:
      relational_database_name: example-database
      availability_zone: us-east-1a
      master_database_name: exampledb
      master_password: examplepassword123
      master_username: exampleuser
      blueprint_id: mysql_8_0
      bundle_id: micro_1_0
```

## Basic PostgreSQL Blueprint

```yaml
resource:
  aws_lightsail_database:
    example:
      relational_database_name: example-database
      availability_zone: us-east-1a
      master_database_name: exampledb
      master_password: examplepassword123
      master_username: exampleuser
      blueprint_id: postgres_12
      bundle_id: micro_1_0
```

## Custom Backup and Maintenance Windows

```yaml
resource:
  aws_lightsail_database:
    example:
      relational_database_name: example-database
      availability_zone: us-east-1a
      master_database_name: exampledb
      master_password: examplepassword123
      master_username: exampleuser
      blueprint_id: postgres_12
      bundle_id: micro_1_0
      preferred_backup_window: "16:00-16:30"
      preferred_maintenance_window: "Tue:17:00-Tue:17:30"
```

## Final Snapshots

```yaml
resource:
  aws_lightsail_database:
    example:
      relational_database_name: example-database
      availability_zone: us-east-1a
      master_database_name: exampledb
      master_password: examplepassword123
      master_username: exampleuser
      blueprint_id: postgres_12
      bundle_id: micro_1_0
      preferred_backup_window: "16:00-16:30"
      preferred_maintenance_window: "Tue:17:00-Tue:17:30"
      final_snapshot_name: example-final-snapshot
```

## Apply Immediately

```yaml
resource:
  aws_lightsail_database:
    example:
      relational_database_name: example-database
      availability_zone: us-east-1a
      master_database_name: exampledb
      master_password: examplepassword123
      master_username: exampleuser
      blueprint_id: postgres_12
      bundle_id: micro_1_0
      apply_immediately: true
```
