# Resource: aws_rds_global_cluster

Manages an RDS Global Cluster, which is an Aurora global database spread across multiple regions. The global database contains a single primary cluster with read-write capability, and a read-only secondary cluster that receives data from the primary cluster through high-speed replication performed by the Aurora storage subsystem.

## Basic Example

```yaml
resource:
  aws_rds_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: aurora
      engine_version: 5.6.mysql_aurora.1.22.2
      database_name: example_db

resource:
  aws_rds_cluster:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      master_username: username
      master_password: somepass123
      database_name: example_db
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      db_subnet_group_name: default

resource:
  aws_rds_cluster_instance:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.primary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default

resource:
  aws_rds_cluster:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      db_subnet_group_name: default
      lifecycle:
        ignore_changes:
          - replication_source_identifier
      depends_on:
        - ${aws_rds_cluster_instance.primary}

resource:
  aws_rds_cluster_instance:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.secondary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default
```

## New PostgreSQL Global Cluster

```yaml
resource:
  aws_rds_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: aurora-postgresql
      engine_version: 11.9
      database_name: example_db

resource:
  aws_rds_cluster:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      master_username: username
      master_password: somepass123
      database_name: example_db
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      db_subnet_group_name: default

resource:
  aws_rds_cluster_instance:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.primary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default

resource:
  aws_rds_cluster:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      skip_final_snapshot: true
      db_subnet_group_name: default
      lifecycle:
        ignore_changes:
          - replication_source_identifier
      depends_on:
        - ${aws_rds_cluster_instance.primary}

resource:
  aws_rds_cluster_instance:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.secondary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default
```

## New Global Cluster From Existing DB Cluster

```yaml
resource:
  aws_rds_cluster:
    example:
      lifecycle:
        ignore_changes: 
          - global_cluster_identifier

resource:
  aws_rds_global_cluster:
    example:
      force_destroy: true
      global_cluster_identifier: example
      source_db_cluster_identifier: ${aws_rds_cluster.example.arn}
```

## Upgrading Engine Versions

```yaml
resource:
  aws_rds_global_cluster:
    example:
      global_cluster_identifier: kyivkharkiv
      engine: aurora-mysql
      engine_version: 5.7.mysql_aurora.2.07.5

resource:
  aws_rds_cluster:
    primary:
      allow_major_version_upgrade: true
      apply_immediately: true
      cluster_identifier: odessadnipro
      database_name: totoro
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      master_password: satsukimae
      master_username: maesatsuki
      skip_final_snapshot: true
      lifecycle:
        ignore_changes: 
          - engine_version

resource:
  aws_rds_cluster_instance:
    primary:
      apply_immediately: true
      cluster_identifier: ${aws_rds_cluster.primary.id}
      engine: ${aws_rds_cluster.primary.engine}
      engine_version: ${aws_rds_cluster.primary.engine_version}
      identifier: donetsklviv
      instance_class: db.r4.large
```

## Argument Reference

The following arguments are required:

* `global_cluster_identifier` - (Required, Forces new resources) Global cluster identifier.

The following arguments are optional:

* `database_name` - (Optional, Forces new resources) Name for an automatically created database on cluster creation. ytofu will only perform drift detection if a configuration value is provided.
* `deletion_protection` - (Optional) If the Global Cluster should have deletion protection enabled. The database can't be deleted when this value is set to `true`. The default is `false`.
* `engine` - (Optional, Forces new resources) Name of the database engine to be used for this DB cluster. ytofu will only perform drift detection if a configuration value is provided. Valid values: `aurora`, `aurora-mysql`, `aurora-postgresql`. Defaults to `aurora`. Conflicts with `source_db_cluster_identifier`.
* `engine_lifecycle_support` - (Optional) The life cycle type for this DB instance. This setting applies only to Aurora PostgreSQL-based global databases. Valid values are `open-source-rds-extended-support`, `open-source-rds-extended-support-disabled`. Default value is `open-source-rds-extended-support`. [Using Amazon RDS Extended Support]: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/extended-support.html
* `engine_version` - (Optional) Engine version of the Aurora global database. The `engine`, `engine_version`, and `instance_class` (on the `aws_rds_cluster_instance`) must together support global databases. See [Using Amazon Aurora global databases](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database.html) for more information. By upgrading the engine version, ytofu will upgrade cluster members. **NOTE:** To avoid an `inconsistent final plan` error while upgrading, use the `lifecycle` `ignore_changes` for `engine_version` meta argument on the associated `aws_rds_cluster` resource as shown above in [Upgrading Engine Versions](#upgrading-engine-versions) example.
* `force_destroy` - (Optional) Enable to remove DB Cluster members from Global Cluster on destroy. Required with `source_db_cluster_identifier`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `source_db_cluster_identifier` - (Optional) Amazon Resource Name (ARN) to use as the primary DB Cluster of the Global Cluster on creation. ytofu cannot perform drift detection of this value. **NOTE:** After initial creation, this argument can be removed and replaced with `engine` and `engine_version`. This allows upgrading the engine version of the Global Cluster.
* `storage_encrypted` - (Optional, Forces new resources) Specifies whether the DB cluster is encrypted. The default is `false` unless `source_db_cluster_identifier` is specified and encrypted. ytofu will only perform drift detection if a configuration value is provided.
* `tags` - (Optional) A map of tags to assign to the DB cluster. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - RDS Global Cluster Amazon Resource Name (ARN).
* `endpoint` - Writer endpoint for the new global database cluster. This endpoint always points to the writer DB instance in the current primary cluster.
* `global_cluster_members` - Set of objects containing Global Cluster members.
    * `db_cluster_arn` - Amazon Resource Name (ARN) of member DB Cluster.
    * `is_writer` - Whether the member is the primary DB Cluster.
* `global_cluster_resource_id` - AWS Region-unique, immutable identifier for the global database cluster. This identifier is found in AWS CloudTrail log entries whenever the AWS KMS key for the DB cluster is accessed.
* `id` - RDS Global Cluster identifier.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `30m`)
- `update` - (Default `90m`)
- `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_rds_global_cluster.example example
```
