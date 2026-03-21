# Resource: aws_glue_resource_policy

Provides a Glue resource policy. Only one can exist per region.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

  aws_partition:
    current:

  aws_region:
    current:

  aws_iam_policy_document:
    glue-example-policy:
      statement:
        actions:
          - "glue:CreateTable"
        resources: 
          - "arn:${data.aws_partition.current.partition}:glue:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:*"
        principals:
          identifiers: 
            - "*"
          type: AWS

resource:
  aws_glue_resource_policy:
    example:
      policy: ${data.aws_iam_policy_document.glue-example-policy.json}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy` - (Required) The policy to be applied to the aws glue data catalog.
* `enable_hybrid` - (Optional) Indicates that you are using both methods to grant cross-account. Valid values are `TRUE` and `FALSE`. Note the terraform will not perform drift detetction on this field as its not return on read.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_glue_resource_policy.Test us-east-1
```
