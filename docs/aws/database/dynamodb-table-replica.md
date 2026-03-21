# Dynamodb Table Replica

Manage Dynamodb Table Replica resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dynamodb_table:
    example:
      name: TestTable
      hash_key: BrodoBaggins
      billing_mode: PAY_PER_REQUEST
      stream_enabled: true
      stream_view_type: NEW_AND_OLD_IMAGES
      attribute:
        name: BrodoBaggins
        type: S
      lifecycle:
        ignore_changes: 
          - replica

resource:
  aws_dynamodb_table_replica:
    example:
      global_table_arn: ${aws_dynamodb_table.example.arn}
      tags:
        Name: IZPAWS
        Pozo: Amargo
```
