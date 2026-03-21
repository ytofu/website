# Codebuild Report Group

Manage Codebuild Report Group resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: Enable IAM User Permissions
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root"
        actions: 
          - "kms:*"
        resources: 
          - "*"

resource:
  aws_kms_key:
    example:
      description: my test kms key
      deletion_window_in_days: 7
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_s3_bucket:
    example:
      bucket: my-test

resource:
  aws_codebuild_report_group:
    example:
      name: my test report group
      type: TEST
      export_config:
        type: S3
        s3_destination:
          bucket: ${aws_s3_bucket.example.id}
          encryption_disabled: false
          encryption_key: ${aws_kms_key.example.arn}
          packaging: NONE
          path: /some
```
