# Resource: aws_redshift_resource_policy

Creates a new Amazon Redshift Resource Policy.

## Basic Example

```yaml
resource:
  aws_redshift_resource_policy:
    example:
      resource_arn: ${aws_redshift_cluster.example.cluster_namespace_arn}
      policy: '{ "Version": "2012-10-17" "Statement": [{ "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::12345678901:root" } "Action": "redshift:CreateInboundIntegration" "Resource": aws_redshift_cluster.example.cluster_namespace_arn "Sid": "" }] }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) The Amazon Resource Name (ARN) of the account to create or update a resource policy for.
* `policy` - (Required) The content of the resource policy being updated.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Resource Name (ARN) of the account to create or update a resource policy for.

## Import

```bash
ytofu import aws_redshift_resource_policy.example example
```
