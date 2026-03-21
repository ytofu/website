# Resource: aws_s3_bucket_metric

Provides a S3 bucket [metrics configuration](http://docs.aws.amazon.com/AmazonS3/latest/dev/metrics-configurations.html) resource.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

  aws_s3_bucket_metric:
    example-entire-bucket:
      bucket: ${aws_s3_bucket.example.id}
      name: EntireBucket```

## Add metrics configuration with S3 object filter

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

  aws_s3_bucket_metric:
    example-filtered:
      bucket: ${aws_s3_bucket.example.id}
      name: ImportantBlueDocuments
      filter:
        prefix: documents/
        tags:
          priority: high
          class: blue```

## Add metrics configuration with S3 object filter for S3 Access Point

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

  aws_s3_access_point:
    example-access-point:
      bucket: ${aws_s3_bucket.example.id}
      name: example-access-point

  aws_s3_bucket_metric:
    example-filtered:
      bucket: ${aws_s3_bucket.example.id}
      name: ImportantBlueDocuments
      filter:
        access_point: ${aws_s3_access_point.example-access-point.arn}
        tags:
          priority: high
          class: blue```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required) Name of the bucket to put metric configuration.
* `name` - (Required) Unique identifier of the metrics configuration for the bucket. Must be less than or equal to 64 characters in length.
* `filter` - (Optional) [Object filtering](http://docs.aws.amazon.com/AmazonS3/latest/dev/metrics-configurations.html#metrics-configurations-filter) that accepts a prefix, tags, or a logical AND of prefix and tags (documented below).

The `filter` metric configuration supports the following:

* `access_point` - (Optional) S3 Access Point ARN for filtering (singular).
* `prefix` - (Optional) Object prefix for filtering (singular).
* `tags` - (Optional) Object tags for filtering (up to 10).

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_s3_bucket_metric.my-bucket-entire-bucket my-bucket:EntireBucket
```
