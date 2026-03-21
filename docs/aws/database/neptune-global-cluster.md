# Resource: aws_neptune_global_cluster

Manages a Neptune Global Cluster. A global cluster consists of one primary region and up to five read-only secondary regions. You issue write operations directly to the primary cluster in the primary region and Amazon Neptune automatically replicates the data to the secondary regions using dedicated infrastructure.

## Basic Example

```yaml
resource:
  aws_neptune_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: neptune
      engine_version: 1.2.0.0

resource:
  aws_neptune_cluster:
    primary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      global_cluster_identifier: ${aws_neptune_global_cluster.example.id}
      neptune_subnet_group_name: default

resource:
  aws_neptune_cluster_instance:
    primary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_neptune_cluster.primary.id}
      instance_class: db.r5.large
      neptune_subnet_group_name: default

resource:
  aws_neptune_cluster:
    secondary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_neptune_global_cluster.example.id}
      neptune_subnet_group_name: default

resource:
  aws_neptune_cluster_instance:
    secondary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_neptune_cluster.secondary.id}
      instance_class: db.r5.large
      neptune_subnet_group_name: default
      depends_on:
        - ${aws_neptune_cluster_instance.primary}
```

## New Global Cluster From Existing DB Cluster

```yaml
resource:
  aws_neptune_cluster:
    example:
      lifecycle:
        ignore_changes: 
          - global_cluster_identifier

resource:
  aws_neptune_global_cluster:
    example:
      global_cluster_identifier: example
      source_db_cluster_identifier: ${aws_neptune_cluster.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `global_cluster_identifier` - (Required, Forces new resources) Global cluster identifier.
* `deletion_protection` - (Optional) If the Global Cluster should have deletion protection enabled. The database can't be deleted when this value is set to `true`. The default is `false`.
* `engine` - (Optional, Forces new resources) Name of the database engine to be used for this DB cluster. ytofu will only perform drift detection if a configuration value is provided. Current Valid values: `neptune`. Conflicts with `source_db_cluster_identifier`.
* `engine_version` - (Optional) Engine version of the global database. Upgrading the engine version will result in all cluster members being immediately updated and will.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `source_db_cluster_identifier` - (Optional) ARN to use as the primary DB Cluster of the Global Cluster on creation. ytofu cannot perform drift detection of this value.
* `storage_encrypted` - (Optional, Forces new resources) Whether the DB cluster is encrypted. The default is `false` unless `source_db_cluster_identifier` is specified and encrypted. ytofu will only perform drift detection if a configuration value is provided.

### Timeouts

The `timeouts` block allows you to specify timeouts for certain actions:

* `create` - (Defaults to 5 mins) Used when creating the Global Cluster
* `update` - (Defaults to 120 mins) Used when updating the Global Cluster members (time is per member)
* `delete` - (Defaults to 5 mins) Used when deleting the Global Cluster members (time is per member)

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Global Cluster ARN
* `global_cluster_members` - Set of objects containing Global Cluster members.
    * `db_cluster_arn` - ARN of member DB Cluster.
    * `is_writer` - Whether the member is the primary DB Cluster.
* `global_cluster_resource_id` - AWS Region-unique, immutable identifier for the global database cluster. This identifier is found in AWS CloudTrail log entries whenever the AWS KMS key for the DB cluster is accessed.
* `id` - Neptune Global Cluster.

## Import

```bash
ytofu import aws_neptune_global_cluster.example example
```
