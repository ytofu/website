# Resource: aws_dynamodb_global_table

Manages [DynamoDB Global Tables V1 (version 2017.11.29)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/globaltables.V1.html). These are layered on top of existing DynamoDB Tables.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the global table. Must match underlying DynamoDB Table names in all regions.
* `replica` - (Required) Underlying DynamoDB Table. At least 1 replica must be defined. See below.

### Nested Fields

#### `replica`

* `region_name` - (Required) AWS region name of replica DynamoDB TableE.g., `us-east-1`

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the DynamoDB Global Table
* `arn` - The ARN of the DynamoDB Global Table

## Import

```bash
ytofu import aws_dynamodb_global_table.MyTable MyTable
```
