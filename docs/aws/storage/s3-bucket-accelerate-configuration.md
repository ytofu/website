# Resource: aws_s3_bucket_accelerate_configuration

Provides an S3 bucket accelerate configuration resource. See the [Requirements for using Transfer Acceleration](https://docs.aws.amazon.com/AmazonS3/latest/userguide/transfer-acceleration.html#transfer-acceleration-requirements) for more details.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    mybucket:
      bucket: mybucket

  aws_s3_bucket_accelerate_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      status: Enabled```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required, Forces new resource) Name of the bucket.
* `status` - (Required) Transfer acceleration state of the bucket. Valid values: `Enabled`, `Suspended`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket` or `bucket` and `expected_bucket_owner` separated by a comma (`,`) if the latter is provided.

## Import

```bash
ytofu import aws_s3_bucket_accelerate_configuration.example bucket-name
```
