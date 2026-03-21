# Resource: aws_docdb_global_cluster

Manages an DocumentDB Global Cluster. A global cluster consists of one primary region and up to five read-only secondary regions. You issue write operations directly to the primary cluster in the primary region and Amazon DocumentDB automatically replicates the data to the secondary regions using dedicated infrastructure.

## Basic Example

```yaml
resource:
  aws_docdb_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: docdb
      engine_version: 4.0.0

resource:
  aws_docdb_cluster:
    primary:
      engine: ${aws_docdb_global_cluster.example.engine}
      engine_version: ${aws_docdb_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      master_username: username
      master_password: somepass123
      global_cluster_identifier: ${aws_docdb_global_cluster.example.id}
      db_subnet_group_name: default

resource:
  aws_docdb_cluster_instance:
    primary:
      engine: ${aws_docdb_global_cluster.example.engine}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_docdb_cluster.primary.id}
      instance_class: db.r5.large

resource:
  aws_docdb_cluster:
    secondary:
      engine: ${aws_docdb_global_cluster.example.engine}
      engine_version: ${aws_docdb_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_docdb_global_cluster.example.id}
      db_subnet_group_name: default
      depends_on:
        - ${aws_docdb_cluster.primary}

resource:
  aws_docdb_cluster_instance:
    secondary:
      engine: ${aws_docdb_global_cluster.example.engine}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_docdb_cluster.secondary.id}
      instance_class: db.r5.large
      depends_on:
        - ${aws_docdb_cluster_instance.primary}
```

## New Global Cluster From Existing DB Cluster

```yaml
resource:
  aws_docdb_cluster:
    example:
      lifecycle:
        ignore_changes: 
          - global_cluster_identifier

resource:
  aws_docdb_global_cluster:
    example:
      global_cluster_identifier: example
      source_db_cluster_identifier: ${aws_docdb_cluster.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `global_cluster_identifier` - (Required, Forces new resources) The global cluster identifier.
* `database_name` - (Optional, Forces new resources) Name for an automatically created database on cluster creation.
* `deletion_protection` - (Optional) If the Global Cluster should have deletion protection enabled. The database can't be deleted when this value is set to `true`. The default is `false`.
* `engine` - (Optional, Forces new resources) Name of the database engine to be used for this DB cluster. ytofu will only perform drift detection if a configuration value is provided. Current Valid values: `docdb`. Defaults to `docdb`. Conflicts with `source_db_cluster_identifier`.
* `engine_version` - (Optional) Engine version of the global database. Upgrading the engine version will result in all cluster members being immediately updated and will.
    * **NOTE:** Upgrading major versions is not supported.
* `source_db_cluster_identifier` - (Optional) Amazon Resource Name (ARN) to use as the primary DB Cluster of the Global Cluster on creation. ytofu cannot perform drift detection of this value.
* `storage_encrypted` - (Optional, Forces new resources) Specifies whether the DB cluster is encrypted. The default is `false` unless `source_db_cluster_identifier` is specified and encrypted. ytofu will only perform drift detection if a configuration value is provided.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Global Cluster Amazon Resource Name (ARN)
* `global_cluster_members` - Set of objects containing Global Cluster members.
    * `db_cluster_arn` - Amazon Resource Name (ARN) of member DB Cluster.
    * `is_writer` - Whether the member is the primary DB Cluster.
* `global_cluster_resource_id` - AWS Region-unique, immutable identifier for the global database cluster. This identifier is found in AWS CloudTrail log entries whenever the AWS KMS key for the DB cluster is accessed.
* `id` - DocumentDB Global Cluster ID.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_docdb_global_cluster.example example
```
