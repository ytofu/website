# SSO Inline Policy

Attach inline policies to permission sets using ytofu YAML.

## Basic Inline Policy

```yaml
data:
  aws_iam_policy_document:
    example:
      statement:
        - effect: Allow
          actions:
            - s3:ListAllMyBuckets
            - s3:GetBucketLocation
          resources:
            - "*"

resource:
  aws_ssoadmin_permission_set_inline_policy:
    example:
      inline_policy: ${data.aws_iam_policy_document.example.json}
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
```
