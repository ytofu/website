# Resource: aws_s3_bucket_policy

Attaches a policy to an S3 bucket resource.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-test-bucket

resource:
  aws_s3_bucket_policy:
    allow_access_from_another_account:
      bucket: ${aws_s3_bucket.example.id}
      policy: ${data.aws_iam_policy_document.allow_access_from_another_account.json}

data:
  aws_iam_policy_document:
    allow_access_from_another_account:
      statement:
        principals:
          type: AWS
          identifiers: 
            - 123456789012
        actions:
          - "s3:GetObject"
          - "s3:ListBucket"
        resources:
          - ${aws_s3_bucket.example.arn}
          - "${aws_s3_bucket.example.arn}/*"
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required) Name of the bucket to which to apply the policy.
* `policy` - (Required) Text of the policy. Although this is a bucket policy rather than an IAM policy, the `aws_iam_policy_document` data source may be used, so long as it specifies a principal. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy). Note: Bucket policies are limited to 20 KB in size.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_s3_bucket_policy.example my-tf-test-bucket
```
