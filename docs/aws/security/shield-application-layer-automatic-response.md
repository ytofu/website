# Resource: aws_shield_application_layer_automatic_response

ytofu resource for managing an AWS Shield Application Layer Automatic Response for automatic DDoS mitigation.

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

## Argument Reference

The following arguments are required:

* `resource_arn` - (Required) ARN of the resource to protect (Cloudfront Distributions and ALBs only at this time).
* `action` - (Required) One of `COUNT` or `BLOCK`

## Attribute Reference

This resource exports no additional attributes.
