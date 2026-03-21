# Resource: aws_dynamodb_table_item

Provides a DynamoDB table item resource

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `hash_key` - (Required) Hash key to use for lookups and identification of the item
* `item` - (Required) JSON representation of a map of attribute name/value pairs, one for each attribute. Only the primary key attributes are required; you can optionally provide other attribute name-value pairs for the item.
* `range_key` - (Optional) Range key to use for lookups and identification of the item. Required if there is range key defined in the table.
* `table_name` - (Required) Name or ARN of the table to contain the item.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:
