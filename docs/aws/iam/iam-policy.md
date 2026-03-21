# Resource: aws_iam_policy

Provides an IAM policy.

## Basic Example

```yaml
resource:
  aws_iam_policy:
    policy:
      name: test_policy
      path: /
      description: My test policy
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "ec2:Describe*", ] "Effect": "Allow" "Resource": "*" }, ] }'
```

## Argument Reference

This resource supports the following arguments:

* `delay_after_policy_creation_in_ms` - (Optional) Number of ms to wait between creating the policy and setting its version as default. May be required in environments with very high S3 IO loads.
* `description` - (Optional, Forces new resource) Description of the IAM policy.
* `name` - (Optional, Forces new resource) Name of the policy. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `path` - (Optional, default "/") Path in which to create the policy. See [IAM Identifiers](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_Identifiers.html) for more information.
* `policy` - (Required) Policy document. This is a JSON formatted string. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy)
* `tags` - (Optional) Map of resource tags for the IAM Policy. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN assigned by AWS to this policy.
* `attachment_count` - Number of entities (users, groups, and roles) that the policy is attached to.
* `id` - ARN assigned by AWS to this policy.
* `policy_id` - Policy's ID.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_iam_policy.administrator arn:aws:iam::123456789012:policy/UsersManageOwnCredentials
```
