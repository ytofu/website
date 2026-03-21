# Dynamodb Tag

Manage Dynamodb Tag resources using ytofu YAML.

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
