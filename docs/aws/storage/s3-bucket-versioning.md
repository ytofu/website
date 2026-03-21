# Resource: aws_s3_bucket_versioning

Provides a resource for controlling versioning on an S3 bucket.
Deleting this resource will either suspend versioning on the associated S3 bucket or
simply remove the resource from ytofu state if the associated S3 bucket is unversioned.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket

  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

  aws_s3_bucket_versioning:
    versioning_example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Enabled```

## With Versioning Disabled

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket

  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

  aws_s3_bucket_versioning:
    versioning_example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Disabled```

## Object Dependency On Versioning

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: yotto

  aws_s3_bucket_versioning:
    example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Enabled

  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket_versioning.example.id}
      key: droeloe
      source: example.txt```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required, Forces new resource) Name of the S3 bucket.
* `versioning_configuration` - (Required) Configuration block for the versioning parameters. [See below](#versioning_configuration).
* `mfa` - (Optional, Required if `versioning_configuration` `mfa_delete` is enabled) Concatenation of the authentication device's serial number, a space, and the value that is displayed on your authentication device.

### versioning_configuration

The `versioning_configuration` configuration block supports the following arguments:

* `status` - (Required) Versioning state of the bucket. Valid values: `Enabled`, `Suspended`, or `Disabled`. `Disabled` should only be used when creating or importing resources that correspond to unversioned S3 buckets.
* `mfa_delete` - (Optional) Specifies whether MFA delete is enabled in the bucket versioning configuration. Valid values: `Enabled` or `Disabled`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket` or `bucket` and `expected_bucket_owner` separated by a comma (`,`) if the latter is provided.

## Import

```bash
ytofu import aws_s3_bucket_versioning.example bucket-name
```
