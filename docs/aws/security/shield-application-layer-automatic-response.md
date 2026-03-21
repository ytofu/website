# Shield Application Layer Automatic Response

Manage Shield Application Layer Automatic Response resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

resource:
  aws_shield_application_layer_automatic_response:
    example:
      resource_arn: "arn:${data.aws_partition.current.partition}:cloudfront:${data.aws_caller_identity.current.account_id}:distribution/example-distribution_id"
      action: COUNT
```
