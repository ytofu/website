# Resource: aws_s3_bucket_object_lock_configuration

Provides an S3 bucket Object Lock configuration resource. For more information about Object Locking, go to [Using S3 Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html) in the Amazon S3 User Guide.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: mybucket

resource:
  aws_s3_bucket_versioning:
    example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket_object_lock_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        default_retention:
          mode: COMPLIANCE
          days: 5
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required, Forces new resource) Name of the bucket.
* `object_lock_enabled` - (Optional, Forces new resource) Indicates whether this bucket has an Object Lock configuration enabled. Defaults to `Enabled`. Valid values: `Enabled`.
* `rule` - (Optional) Configuration block for specifying the Object Lock rule for the specified object. [See below](#rule).
* `token` - (Optional,Deprecated) This argument is deprecated and no longer needed to enable Object Lock.
To enable Object Lock for an existing bucket, you must first enable versioning on the bucket and then enable Object Lock. For more details on versioning, see the [`aws_s3_bucket_versioning` resource](s3_bucket_versioning.html.markdown).

### rule

The `rule` configuration block supports the following arguments:

* `default_retention` - (Required) Configuration block for specifying the default Object Lock retention settings for new objects placed in the specified bucket. [See below](#default_retention).

### default_retention

The `default_retention` configuration block supports the following arguments:

* `days` - (Optional, Required if `years` is not specified) Number of days that you want to specify for the default retention period.
* `mode` - (Required) Default Object Lock retention mode you want to apply to new objects placed in the specified bucket. Valid values: `COMPLIANCE`, `GOVERNANCE`.
* `years` - (Optional, Required if `days` is not specified) Number of years that you want to specify for the default retention period.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket` or `bucket` and `expected_bucket_owner` separated by a comma (`,`) if the latter is provided.

## Import

```bash
ytofu import aws_s3_bucket_object_lock_configuration.example bucket-name
```
