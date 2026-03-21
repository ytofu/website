# Resource: aws_dynamodb_tag

Manages an individual DynamoDB resource tag. This resource should only be used in cases where DynamoDB resources are created outside ytofu (e.g., Table replicas in other regions).

## Basic Example

```yaml
data:
  aws_region:
    replica:

data:
  aws_region:
    current:

resource:
  aws_dynamodb_table:
    example:
      replica:
        region_name: ${data.aws_region.replica.name}

resource:
  aws_dynamodb_tag:
    test:
      resource_arn: replaced-value
      key: testkey
      value: testvalue
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) Amazon Resource Name (ARN) of the DynamoDB resource to tag.
* `key` - (Required) Tag name.
* `value` - (Required) Tag value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - DynamoDB resource identifier and key, separated by a comma (`,`)

## Import

```bash
ytofu import aws_dynamodb_tag.example arn:aws:dynamodb:us-east-1:123456789012:table/example,Name
```
