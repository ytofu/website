# Resource: aws_s3control_bucket_policy

Provides a resource to manage an S3 Control Bucket Policy.

## Basic Example

```yaml
resource:
  aws_s3control_bucket_policy:
    example:
      bucket: ${aws_s3control_bucket.example.arn}
      policy: '{ "Id": "testBucketPolicy" "Statement": [ { "Action": "s3-outposts:PutBucketLifecycleConfiguration" "Effect": "Deny" "Principal": { "AWS": "*" } "Resource": aws_s3control_bucket.example.arn "Sid": "statement1" } ] "Version": "2012-10-17" }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required) Amazon Resource Name (ARN) of the bucket.
* `policy` - (Required) JSON string of the resource policy. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Resource Name (ARN) of the bucket.

## Import

```bash
ytofu import aws_s3control_bucket_policy.example arn:aws:s3-outposts:us-east-1:123456789012:outpost/op-12345678/bucket/example
```
