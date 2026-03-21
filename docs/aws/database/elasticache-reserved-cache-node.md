# Resource: aws_elasticache_reserved_cache_node

Manages an ElastiCache Reserved Cache Node.

## Basic Example

```yaml
data:
  aws_elasticache_reserved_cache_node_offering:
    example:
      cache_node_type: cache.t4g.small
      duration: P1Y
      offering_type: No Upfront
      product_description: redis

resource:
  aws_elasticache_reserved_cache_node:
    example:
      reserved_cache_nodes_offering_id: ${data.aws_elasticache_reserved_cache_node_offering.example.offering_id}
      id: optionalCustomReservationID
      cache_node_count: 3
```

## Argument Reference

The following arguments are required:

* `reserved_cache_nodes_offering_id` - (Required) ID of the reserved cache node offering to purchase.
  To determine an `reserved_cache_nodes_offering_id`, see the `aws_elasticache_reserved_cache_node_offering` data source.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cache_node_count` - (Optional) Number of cache node instances to reserve.
  Default value is `1`.
* `id` - (Optional) Customer-specified identifier to track this reservation.
  If not specified, AWS will assign a random ID.
* `tags` - (Optional) Map of tags to assign to the reservation. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN for the reserved cache node.
* `duration` - Duration of the reservation as an RFC3339 duration.
* `fixed_price` - Fixed price charged for this reserved cache node.
* `cache_node_type` - Node type for the reserved cache nodes.
* `offering_type` - Offering type of this reserved cache node.
* `product_description` - Engine type for the reserved cache node.
* `recurring_charges` - Recurring price charged to run this reserved cache node.
* `start_time` - Time the reservation started.
* `state` - State of the reserved cache node.
* `usage_price` - Hourly price charged for this reserved cache node.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `30m`)
- `update` - (Default `10m`)
- `delete` - (Default `1m`)

## Import

```bash
ytofu import aws_elasticache_reserved_cache_node.example CustomReservationID
```
