# Resource: aws_finspace_kx_user

ytofu resource for managing an AWS FinSpace Kx User.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: Example KMS Key
      deletion_window_in_days: 7

  aws_finspace_kx_environment:
    example:
      name: my-tf-kx-environment
      kms_key_id: ${aws_kms_key.example.arn}

  aws_iam_role:
    example:
      name: example-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "ec2.amazonaws.com" } }, ] }'

  aws_finspace_kx_user:
    example:
      name: my-tf-kx-user
      environment_id: ${aws_finspace_kx_environment.example.id}
      iam_role: ${aws_iam_role.example.arn}```

## Argument Reference

The following arguments are required:

* `name` - (Required) A unique identifier for the user.
* `environment_id` - (Required) Unique identifier for the KX environment.
* `iam_role` - (Required) IAM role ARN to be associated with the user.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) identifier of the KX user.
* `id` - A comma-delimited string joining environment ID and user name.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_finspace_kx_user.example n3ceo7wqxoxcti5tujqwzs,my-tf-kx-user
```
