# Dynamodb Global Table

Manage Dynamodb Global Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dynamodb_table:
    us-east-1:
      hash_key: myAttribute
      name: myTable
      stream_enabled: true
      stream_view_type: NEW_AND_OLD_IMAGES
      read_capacity: 1
      write_capacity: 1
      attribute:
        name: myAttribute
        type: S

resource:
  aws_dynamodb_table:
    us-west-2:
      hash_key: myAttribute
      name: myTable
      stream_enabled: true
      stream_view_type: NEW_AND_OLD_IMAGES
      read_capacity: 1
      write_capacity: 1
      attribute:
        name: myAttribute
        type: S

resource:
  aws_dynamodb_global_table:
    myTable:
      depends_on:
        - ${aws_dynamodb_table.us-east-1}
        - ${aws_dynamodb_table.us-west-2}
      name: myTable
      replica:
        region_name: us-east-1
      replica:
        region_name: us-west-2
```
