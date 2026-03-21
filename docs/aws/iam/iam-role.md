# IAM Role

Manage IAM Role resources using ytofu YAML.

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
