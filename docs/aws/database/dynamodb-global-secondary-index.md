# Dynamodb Global Secondary Index

Manage Dynamodb Global Secondary Index resources using ytofu YAML.

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

resource:
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
        type: S
```
