# Resource: aws_elasticache_global_replication_group

Provides an ElastiCache Global Replication Group resource, which manages replication between two or more Replication Groups in different regions. For more information, see the [ElastiCache User Guide](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Redis-Global-Datastore.html).

## Basic Example

```yaml
resource:
  aws_elasticache_global_replication_group:
    example:
      global_replication_group_id_suffix: example
      primary_replication_group_id: ${aws_elasticache_replication_group.primary.id}

  aws_elasticache_replication_group:
    primary:
      replication_group_id: example-primary
      description: primary replication group
      engine: redis
      engine_version: 5.0.6
      node_type: cache.m5.large
      num_cache_clusters: 1

  aws_elasticache_replication_group:
    secondary:
      replication_group_id: example-secondary
      description: secondary replication group
      global_replication_group_id: ${aws_elasticache_global_replication_group.example.global_replication_group_id}
      num_cache_clusters: 1```

## Managing Redis OOS/Valkey Engine Versions

```yaml
resource:
  aws_elasticache_global_replication_group:
    example:
      global_replication_group_id_suffix: example
      primary_replication_group_id: ${aws_elasticache_replication_group.primary.id}
      engine_version: 6.2

  aws_elasticache_replication_group:
    primary:
      replication_group_id: example-primary
      description: primary replication group
      engine: redis
      engine_version: 6.0
      node_type: cache.m5.large
      num_cache_clusters: 1

  aws_elasticache_replication_group:
    secondary:
      replication_group_id: example-secondary
      description: secondary replication group
      global_replication_group_id: ${aws_elasticache_global_replication_group.example.global_replication_group_id}
      num_cache_clusters: 1```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `automatic_failover_enabled` - (Optional) Specifies whether read-only replicas will be automatically promoted to read/write primary if the existing primary fails.
  When creating, by default the Global Replication Group inherits the automatic failover setting of the primary replication group.
* `cache_node_type` - (Optional) The instance class used.
  See AWS documentation for information on [supported node types](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/CacheNodes.SupportedTypes.html)
  and [guidance on selecting node types](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/nodes-select-size.html).
  When creating, by default the Global Replication Group inherits the node type of the primary replication group.
* `engine` - (Optional) The name of the cache engine to be used for the clusters in this global replication group.
  When creating, by default the Global Replication Group inherits the engine of the primary replication group.
  If an engine is specified, the Global Replication Group and all member replication groups will be upgraded to this engine.
  Valid values are `redis` or `valkey`.
  Default is `redis` if `engine_version` is specified.
* `engine_version` - (Optional) Engine version to use for the Global Replication Group.
  When creating, by default the Global Replication Group inherits the version of the primary replication group.
  If a version is specified, the Global Replication Group and all member replication groups will be upgraded to this version.
  Cannot be downgraded without replacing the Global Replication Group and all member replication groups.
  When the version is 7 or higher, the major and minor version should be set, e.g., `7.2`.
  When the version is 6, the major and minor version can be set, e.g., `6.2`,
  or the minor version can be unspecified which will use the latest version at creation time, e.g., `6.x`.
  The actual engine version used is returned in the attribute `engine_version_actual`, see [Attribute Reference](#attribute-reference) below.
* `global_replication_group_id_suffix` - (Required) The suffix name of a Global Datastore. If `global_replication_group_id_suffix` is changed, creates a new resource.
* `primary_replication_group_id` - (Required) The ID of the primary cluster that accepts writes and will replicate updates to the secondary cluster. If `primary_replication_group_id` is changed, creates a new resource.
* `global_replication_group_description` - (Optional) A user-created description for the global replication group.
* `num_node_groups` - (Optional) The number of node groups (shards) on the global replication group.
* `parameter_group_name` - (Optional) An ElastiCache Parameter Group to use for the Global Replication Group.
  Required when upgrading an engine or major engine version, but will be ignored if left configured after the upgrade is complete.
  Specifying without a major version upgrade will fail.
  Note that ElastiCache creates a copy of this parameter group for each member replication group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the ElastiCache Global Replication Group.
* `arn` - The ARN of the ElastiCache Global Replication Group.
* `engine_version_actual` - The full version number of the cache engine running on the members of this global replication group.
* `at_rest_encryption_enabled` - A flag that indicate whether the encryption at rest is enabled.
* `auth_token_enabled` - A flag that indicate whether AuthToken (password) is enabled.
* `cluster_enabled` - Indicates whether the Global Datastore is cluster enabled.
* `global_replication_group_id` - The full ID of the global replication group.
* `global_node_groups` - Set of node groups (shards) on the global replication group.
  Has the values:
    * `global_node_group_id` - The ID of the global node group.
    * `slots` - The keyspace for this node group.
* `transit_encryption_enabled` - A flag that indicates whether the encryption in transit is enabled.

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `update` - (Default `60m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_elasticache_global_replication_group.my_global_replication_group okuqm-global-replication-group-1
```
