# Resource: aws_iam_role

Provides an IAM role.

## Basic Example

```yaml
resource:
  aws_iam_role:
    test_role:
      name: test_role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "ec2.amazonaws.com" } }, ] }'
      tags:
        tag-key: tag-value
```

## Example of Using Data Source for Assume Role Policy

```yaml
data:
  aws_iam_policy_document:
    instance_assume_role_policy:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - ec2.amazonaws.com

resource:
  aws_iam_role:
    instance:
      name: instance_role
      path: /system/
      assume_role_policy: ${data.aws_iam_policy_document.instance_assume_role_policy.json}
```

## Example of Exclusive Inline Policies

```yaml
resource:
  aws_iam_role:
    example:
      name: yak_role
      assume_role_policy: ${data.aws_iam_policy_document.instance_assume_role_policy.json}
      inline_policy:
        name: my_inline_policy
        policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["ec2:Describe*"] "Effect": "Allow" "Resource": "*" }, ] }'
      inline_policy:
        name: policy-8675309
        policy: ${data.aws_iam_policy_document.inline_policy.json}

data:
  aws_iam_policy_document:
    inline_policy:
      statement:
        actions: 
          - "ec2:DescribeAccountAttributes"
        resources: 
          - "*"
```

## Example of Removing Inline Policies

```yaml
resource:
  aws_iam_role:
    example:
      name: yak_role
      assume_role_policy: ${data.aws_iam_policy_document.instance_assume_role_policy.json}
      inline_policy:
```

## Example of Exclusive Managed Policies

```yaml
resource:
  aws_iam_role:
    example:
      name: yak_role
      assume_role_policy: ${data.aws_iam_policy_document.instance_assume_role_policy.json}
      managed_policy_arns: 
        - ${aws_iam_policy.policy_one.arn}
        - ${aws_iam_policy.policy_two.arn}

resource:
  aws_iam_policy:
    policy_one:
      name: policy-618033
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["ec2:Describe*"] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_iam_policy:
    policy_two:
      name: policy-381966
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["s3:ListAllMyBuckets", "s3:ListBucket", "s3:HeadBucket"] "Effect": "Allow" "Resource": "*" }, ] }'
```

## Example of Removing Managed Policies

```yaml
resource:
  aws_iam_role:
    example:
      name: yak_role
      assume_role_policy: ${data.aws_iam_policy_document.instance_assume_role_policy.json}
      managed_policy_arns: []
```

## Argument Reference

The following arguments are required:

* `assume_role_policy` - (Required) Policy that grants an entity permission to assume the role.

The following arguments are optional:

* `description` - (Optional) Description of the role.
* `force_detach_policies` - (Optional) Whether to force detaching any policies the role has before destroying it. Defaults to `false`.
* `max_session_duration` - (Optional) Maximum session duration (in seconds) that you want to set for the specified role. If you do not specify a value for this setting, the default maximum of one hour is applied. This setting can have a value from 1 hour to 12 hours.
* `name` - (Optional, Forces new resource) Friendly name of the role. If omitted, ytofu will assign a random, unique name. See [IAM Identifiers](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_Identifiers.html) for more information.
* `name_prefix` - (Optional, Forces new resource) Creates a unique friendly name beginning with the specified prefix. Conflicts with `name`.
* `path` - (Optional) Path to the role. See [IAM Identifiers](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_Identifiers.html) for more information.
* `permissions_boundary` - (Optional) ARN of the policy that is used to set the permissions boundary for the role.
* `tags` - Key-value mapping of tags for the IAM role. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### inline_policy

This configuration block supports the following:

* `name` - (Required) Name of the role policy.
* `policy` - (Required) Policy document as a JSON formatted string. For more information about building IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/tutorials/terraform/aws-iam-policy).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) specifying the role.
* `create_date` - Creation date of the IAM role.
* `id` - Name of the role.
* `name` - Name of the role.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `unique_id` - Stable and unique string identifying the role.

## Import

```bash
ytofu import aws_iam_role.example developer_name
```
