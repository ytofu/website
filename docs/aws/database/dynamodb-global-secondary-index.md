# Resource: aws_dynamodb_global_secondary_index

!> The resource type `aws_dynamodb_global_secondary_index` is an experimental feature. The schema or behavior may change without notice, and it is not subject to the backwards compatibility guarantee of the provider.

## Basic Example

```yaml
resource:
  aws_dynamodb_global_secondary_index:
    example:
      table_name: ${aws_dynamodb_table.example.name}
      index_name: GameTitleIndex
      projection:
        projection_type: INCLUDE
        non_key_attributes: 
          - UserId
      provisioned_throughput:
        write_capacity_units: 10
        read_capacity_units: 10
      key_schema:
        attribute_name: GameTitle
        attribute_type: S
        key_type: HASH

  aws_dynamodb_table:
    example:
      name: example
      billing_mode: PROVISIONED
      read_capacity: 20
      write_capacity: 20
      hash_key: UserId
      range_key: GameTitle
      attribute:
        name: UserId
        type: S
      attribute:
        name: GameTitle
        type: S```

## Argument Reference

The following arguments are required:

* `index_name` - (Required) Name of the index.
* `key_schema` - (Required) Set of nested attribute definitions.
  At least 1 element defining a `HASH` is required.
  All elements with the `key_type` of `HASH` must precede elements with `key_type` of `RANGE`.
  Changing any values in `key_schema` will re-create the resource.
  See [`key_schema` below](#key_schema).
* `projection` - (Required) Describes which attributes from the table are represented in the index.
  See [`projection` below](#projection).
* `table_name` - (Required) Name of the table this index belongs to.

The following arguments are optional:

* `on_demand_throughput` - (Optional) Sets the maximum number of read and write units for the index.
  See [`on_demand_throughput` below](#on_demand_throughput).
  Only valid if the table's `billing_mode` is `PAY_PER_REQUEST`.
* `provisioned_throughput` - (Optional) Provisioned throughput for the index.
  See [`provisioned_throughput` below](#provisioned_throughput).
  Required if the table's `billing_mode` is `PROVISIONED`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `warm_throughput` - (Optional) Sets the number of warm read and write units for this index.
  See [`warm_throughput` below](#warm_throughput).

### `key_schema`

* `attribute_name` - (Required) Name of the attribute.
* `attribute_type` - (Required) Type of the attribute in the index.
  Valid values are `S` (string), `N` (number), or `B` (binary).
* `key_type` - (Required) Key type.
  Valid values are `HASH` or `RANGE`.

### `on_demand_throughput`

* `max_read_request_units` - (Optional) Maximum number of read request units for this index.
* `max_write_request_units` - (Optional) Maximum number of write request units for this index.

### `projection`

* `non_key_attributes` - (Optional) Specifies which additional attributes to include in the index.
  Only valid when `projection_type` is `INCLUDE`.`
* `projection_type` - (Required) The set of attributes represented in the index.
  One of `ALL`, `INCLUDE`, or `KEYS_ONLY`.

### `provisioned_throughput`

* `read_capacity_units` - (Required) Number of read capacity units for this index.
* `write_capacity_units` - (Required) Number of write capacity units for this index.

### `warm_throughput`

* `read_units_per_second` - (Required) Number of read operations this index can instantaneously support.
* `write_units_per_second` - (Required) Number of write operations this index can instantaneously support.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the GSI.

## Import

```bash
ytofu import aws_dynamodb_global_secondary_index.example 'example-table,example-index'
```
