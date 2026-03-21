# Redshiftdata Statement

Manage Redshiftdata Statement resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshiftdata_statement:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.cluster_identifier}
      database: ${aws_redshift_cluster.example.database_name}
      db_user: ${aws_redshift_cluster.example.master_username}
      sql: CREATE GROUP group_name;
```

## workgroup_name

```yaml
resource:
  aws_redshiftdata_statement:
    example:
      workgroup_name: ${aws_redshiftserverless_workgroup.example.workgroup_name}
      database: dev
      sql: CREATE GROUP group_name;
```
