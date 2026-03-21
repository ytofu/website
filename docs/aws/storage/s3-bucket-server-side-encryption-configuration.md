# Resource: aws_s3_bucket_server_side_encryption_configuration

Provides a S3 bucket server-side encryption configuration resource.

## Basic Example

```yaml
resource:
  aws_kms_key:
    mykey:
      description: This key is used to encrypt bucket objects
      deletion_window_in_days: 10

resource:
  aws_s3_bucket:
    mybucket:
      bucket: mybucket

resource:
  aws_s3_bucket_server_side_encryption_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      rule:
        apply_server_side_encryption_by_default:
          kms_master_key_id: ${aws_kms_key.mykey.arn}
          sse_algorithm: "aws:kms"
```

## Blocking SSE-C Uploads

```yaml
resource:
  aws_kms_key:
    mykey:
      description: This key is used to encrypt bucket objects
      deletion_window_in_days: 10

resource:
  aws_s3_bucket:
    mybucket:
      bucket: mybucket

resource:
  aws_s3_bucket_server_side_encryption_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      rule:
        apply_server_side_encryption_by_default:
          kms_master_key_id: ${aws_kms_key.mykey.arn}
          sse_algorithm: "aws:kms"
        bucket_key_enabled: true
        blocked_encryption_types: 
          - SSE-C
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required, Forces new resource) ID (name) of the bucket.
* `rule` - (Required) Set of server-side encryption configuration rules. [See below](#rule). Currently, only a single rule is supported.

### rule

The `rule` configuration block supports the following arguments:

* `apply_server_side_encryption_by_default` - (Optional) Single object for setting server-side encryption by default. [See below](#apply_server_side_encryption_by_default).
* `blocked_encryption_types` - (Optional) List of server-side encryption types to block for object uploads. Valid values are `SSE-C` (blocks uploads using server-side encryption with customer-provided keys) and `NONE` (unblocks all encryption types). Starting in March 2026, Amazon S3 will automatically block SSE-C uploads for all new buckets.
* `bucket_key_enabled` - (Optional) Whether or not to use [Amazon S3 Bucket Keys](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-key.html) for SSE-KMS.

### apply_server_side_encryption_by_default

The `apply_server_side_encryption_by_default` configuration block supports the following arguments:

* `sse_algorithm` - (Required) Server-side encryption algorithm to use. Valid values are `AES256`, `aws:kms`, and `aws:kms:dsse`
* `kms_master_key_id` - (Optional) AWS KMS master key ID used for the SSE-KMS encryption. This can only be used when you set the value of `sse_algorithm` as `aws:kms`. The default `aws/s3` AWS KMS master key is used if this element is absent while the `sse_algorithm` is `aws:kms`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket` or `bucket` and `expected_bucket_owner` separated by a comma (`,`) if the latter is provided.

## Import

```bash
ytofu import aws_s3_bucket_server_side_encryption_configuration.example bucket-name
```
