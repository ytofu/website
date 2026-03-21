# Resource: aws_s3_bucket_request_payment_configuration

Provides an S3 bucket request payment configuration resource. For more information, see [Requester Pays Buckets](https://docs.aws.amazon.com/AmazonS3/latest/dev/RequesterPaysBuckets.html).

## Basic Example

```yaml
resource:
  aws_s3_bucket_request_payment_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      payer: Requester
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required, Forces new resource) Name of the bucket.
* `payer` - (Required) Specifies who pays for the download and request fees. Valid values: `BucketOwner`, `Requester`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket` or `bucket` and `expected_bucket_owner` separated by a comma (`,`) if the latter is provided.

## Import

```bash
ytofu import aws_s3_bucket_request_payment_configuration.example bucket-name
```
