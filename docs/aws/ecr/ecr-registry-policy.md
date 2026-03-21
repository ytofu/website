# Resource: aws_ecr_registry_policy

Provides an Elastic Container Registry Policy.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

  aws_region:
    current:

  aws_partition:
    current:

resource:
  aws_ecr_registry_policy:
    example:
      policy: '{ "Version": "2012-10-17", "Statement": [ { "Sid": "testpolicy", "Effect": "Allow", "Principal": { "AWS" : "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root" }, "Action": [ "ecr:ReplicateImage" ], "Resource": [ "arn:${data.aws_partition.current.partition}:ecr:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:repository/*" ] } ] }'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy` - (Required) The policy document. This is a JSON formatted string. For more information about building IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy)

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `registry_id` - The registry ID where the registry was created.

## Import

```bash
ytofu import aws_ecr_registry_policy.example 123456789012
```
