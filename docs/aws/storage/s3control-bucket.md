# Resource: aws_s3control_bucket

Provides a resource to manage an S3 Control Bucket.

## Basic Example

```yaml
resource:
  aws_s3control_bucket:
    example:
      bucket: example
      outpost_id: ${data.aws_outposts_outpost.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required) Name of the bucket.
* `outpost_id` - (Required) Identifier of the Outpost to contain this bucket.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the bucket.
* `creation_date` - UTC creation date in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8).
* `id` - Amazon Resource Name (ARN) of the bucket.
* `public_access_block_enabled` - Boolean whether Public Access Block is enabled.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_s3control_bucket.example arn:aws:s3-outposts:us-east-1:123456789012:outpost/op-12345678/bucket/example
```
