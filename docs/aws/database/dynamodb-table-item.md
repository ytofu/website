# Dynamodb Table Item

Manage Dynamodb Table Item resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dynamodb_table_item:
    example:
      table_name: ${aws_dynamodb_table.example.name}
      hash_key: ${aws_dynamodb_table.example.hash_key}
      item: |
        {
        "exampleHashKey": {"S": "something"},
        "one": {"N": "11111"},
        "two": {"N": "22222"},
        "three": {"N": "33333"},
        "four": {"N": "44444"}
        }

resource:
  aws_dynamodb_table:
    example:
      name: example-name
      read_capacity: 10
      write_capacity: 10
      hash_key: exampleHashKey
      attribute:
        name: exampleHashKey
        type: S
```
