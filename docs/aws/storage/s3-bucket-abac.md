# Resource: aws_s3_bucket_abac

Manages ABAC (Attribute Based Access Control) for an AWS S3 (Simple Storage) Bucket.
See the [AWS documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/buckets-tagging-enable-abac.html) on enabling ABAC for general purpose buckets for additional information.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: bucket-name

resource:
  aws_s3_bucket_abac:
    example:
      bucket: ${aws_s3_bucket.example.bucket}
      abac_status:
        status: Enabled
```

## Argument Reference

The following arguments are required:

* `bucket` - (Required) General purpose bucket that you want to create the metadata configuration for.
* `abac_status` - (Required) ABAC status configuration. See [`abac_status` Block](#abac_status-block) for details.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

### `abac_status` Block

The `abac_status` configuration block supports the following arguments:

* `status` - (Required) ABAC status of the general purpose bucket.
Valid values are `Enabled` and `Disabled`.
By default, ABAC is disabled for all Amazon S3 general purpose buckets.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_s3_bucket_abac.example bucket-name
```
