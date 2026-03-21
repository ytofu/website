# DB Instance Automated Backups Replication

Manage DB Instance Automated Backups Replication resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_db_instance_automated_backups_replication:
    default:
      source_db_instance_arn: "arn:aws:rds:us-west-2:123456789012:db:mydatabase"
      retention_period: 14
```
