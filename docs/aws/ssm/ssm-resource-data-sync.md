# SSM Resource Data Sync

Manage SSM Resource Data Sync resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    hoge:
      bucket: tf-test-bucket-1234

data:
  aws_iam_policy_document:
    hoge:
      statement:
        sid: SSMBucketPermissionsCheck
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - ssm.amazonaws.com
        actions: 
          - "s3:GetBucketAcl"
        resources: 
          - "arn:aws:s3:::tf-test-bucket-1234"
      statement:
        sid: SSMBucketDelivery
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - ssm.amazonaws.com
        actions: 
          - "s3:PutObject"
        resources: 
          - "arn:aws:s3:::tf-test-bucket-1234/*"
        condition:
          test: StringEquals
          values: 
            - bucket-owner-full-control

resource:
  aws_s3_bucket_policy:
    hoge:
      bucket: ${aws_s3_bucket.hoge.id}
      policy: ${data.aws_iam_policy_document.hoge.json}

resource:
  aws_ssm_resource_data_sync:
    foo:
      name: foo
      s3_destination:
        bucket_name: ${aws_s3_bucket.hoge.bucket}
        region: ${aws_s3_bucket.hoge.region}
```
