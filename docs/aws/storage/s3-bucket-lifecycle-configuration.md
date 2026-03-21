# Resource: aws_s3_bucket_lifecycle_configuration

Provides an independent configuration resource for S3 bucket [lifecycle configuration](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html).

## Basic Example

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: rule-1
        status: Enabled
```

## Specifying an empty filter

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: rule-1
        filter:
          status: Enabled
```

## Specifying a filter using key prefixes

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: rule-1
        filter:
          prefix: logs/
        status: Enabled
```

## Specifying a filter based on an object tag

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: rule-1
        filter:
          tag:
            key: Name
            value: Staging
        status: Enabled
```

## Specifying a filter based on multiple tags

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: rule-1
        filter:
          and:
            tags:
              Key1: Value1
              Key2: Value2
        status: Enabled
```

## Specifying a filter based on both prefix and one or more tags

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: rule-1
        filter:
          and:
            prefix: logs/
            tags:
              Key1: Value1
              Key2: Value2
        status: Enabled
```

## Specifying a filter based on object size

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: Allow small object transitions
        filter:
          object_size_greater_than: 1
        status: Enabled
        transition:
          days: 365
          storage_class: GLACIER_IR
```

## Specifying a filter based on object size range and prefix

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: rule-1
        filter:
          and:
            prefix: logs/
            object_size_greater_than: 500
            object_size_less_than: 64000
        status: Enabled
```

## Creating a Lifecycle Configuration for a bucket with versioning

```yaml
resource:
  aws_s3_bucket:
    bucket:
      bucket: my-bucket

resource:
  aws_s3_bucket_acl:
    bucket_acl:
      bucket: ${aws_s3_bucket.bucket.bucket}
      acl: private

resource:
  aws_s3_bucket_lifecycle_configuration:
    bucket-config:
      bucket: ${aws_s3_bucket.bucket.bucket}
      rule:
        id: log
        expiration:
          days: 90
        filter:
          and:
            prefix: log/
            tags:
              rule: log
              autoclean: true
        status: Enabled
        transition:
          days: 30
          storage_class: STANDARD_IA
        transition:
          days: 60
          storage_class: GLACIER
      rule:
        id: tmp
        filter:
          prefix: tmp/
        expiration:
          date: "2023-01-13T00:00:00Z"
        status: Enabled

resource:
  aws_s3_bucket:
    versioning_bucket:
      bucket: my-versioning-bucket

resource:
  aws_s3_bucket_acl:
    versioning_bucket_acl:
      bucket: ${aws_s3_bucket.versioning_bucket.bucket}
      acl: private

resource:
  aws_s3_bucket_versioning:
    versioning:
      bucket: ${aws_s3_bucket.versioning_bucket.bucket}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket_lifecycle_configuration:
    versioning-bucket-config:
      depends_on: 
        - ${aws_s3_bucket_versioning.versioning}
      bucket: ${aws_s3_bucket.versioning_bucket.bucket}
      rule:
        id: config
        filter:
          prefix: config/
        noncurrent_version_expiration:
          noncurrent_days: 90
        noncurrent_version_transition:
          noncurrent_days: 30
          storage_class: STANDARD_IA
        noncurrent_version_transition:
          noncurrent_days: 60
          storage_class: GLACIER
        status: Enabled
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required) Name of the source S3 bucket you want Amazon S3 to monitor.
* `rule` - (Required) List of configuration blocks describing the rules managing the replication. [See below](#rule).
* `transition_default_minimum_object_size` - (Optional) The default minimum object size behavior applied to the lifecycle configuration. Valid values: `all_storage_classes_128K` (default), `varies_by_storage_class`. To customize the minimum object size for any transition you can add a `filter` that specifies a custom `object_size_greater_than` or `object_size_less_than` value. Custom filters always take precedence over the default transition behavior.

### rule

The `rule` configuration block supports the following arguments:

* `abort_incomplete_multipart_upload` - (Optional) Configuration block that specifies the days since the initiation of an incomplete multipart upload that Amazon S3 will wait before permanently removing all parts of the upload. [See below](#abort_incomplete_multipart_upload).
* `expiration` - (Optional) Configuration block that specifies the expiration for the lifecycle of the object in the form of date, days and, whether the object has a delete marker. [See below](#expiration).
* `filter` - (Optional) Configuration block used to identify objects that a Lifecycle Rule applies to.
  [See below](#filter).
* `id` - (Required) Unique identifier for the rule. The value cannot be longer than 255 characters.
* `noncurrent_version_expiration` - (Optional) Configuration block that specifies when noncurrent object versions expire. [See below](#noncurrent_version_expiration).
* `noncurrent_version_transition` - (Optional) Set of configuration blocks that specify the transition rule for the lifecycle rule that describes when noncurrent objects transition to a specific storage class. [See below](#noncurrent_version_transition).
* `prefix` - (Optional) **DEPRECATED** Use `filter` instead.
  This has been deprecated by Amazon S3.
  Prefix identifying one or more objects to which the rule applies.
* `status` - (Required) Whether the rule is currently being applied. Valid values: `Enabled` or `Disabled`.
* `transition` - (Optional) Set of configuration blocks that specify when an Amazon S3 object transitions to a specified storage class. [See below](#transition).

### abort_incomplete_multipart_upload

The `abort_incomplete_multipart_upload` configuration block supports the following arguments:

* `days_after_initiation` - Number of days after which Amazon S3 aborts an incomplete multipart upload.

### expiration

The `expiration` configuration block supports the following arguments:

* `date` - (Optional) Date the object is to be moved or deleted. The date value must be in [RFC3339 full-date format](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) e.g. `2023-08-22`.
* `days` - (Optional) Lifetime, in days, of the objects that are subject to the rule. The value must be a non-zero positive integer.
* `expired_object_delete_marker` - (Optional, Conflicts with `date` and `days`) Indicates whether Amazon S3 will remove a delete marker with no noncurrent versions. If set to `true`, the delete marker will be expired; if set to `false` the policy takes no action.

### filter

The `filter` configuration block supports the following arguments:

* `and`- (Optional) Configuration block used to apply a logical `AND` to two or more predicates. [See below](#and). The Lifecycle Rule will apply to any object matching all the predicates configured inside the `and` block.
* `object_size_greater_than` - (Optional) Minimum object size (in bytes) to which the rule applies.
* `object_size_less_than` - (Optional) Maximum object size (in bytes) to which the rule applies.
* `prefix` - (Optional) Prefix identifying one or more objects to which the rule applies. Defaults to an empty string (`""`) if not specified.
* `tag` - (Optional) Configuration block for specifying a tag key and value. [See below](#tag).

### noncurrent_version_expiration

The `noncurrent_version_expiration` configuration block supports the following arguments:

* `newer_noncurrent_versions` - (Optional) Number of noncurrent versions Amazon S3 will retain. Must be a non-zero positive integer.
* `noncurrent_days` - (Required) Number of days an object is noncurrent before Amazon S3 can perform the associated action. Must be a positive integer.

### noncurrent_version_transition

The `noncurrent_version_transition` configuration block supports the following arguments:

* `newer_noncurrent_versions` - (Optional) Number of noncurrent versions Amazon S3 will retain. Must be a non-zero positive integer.
* `noncurrent_days` - (Required) Number of days an object is noncurrent before Amazon S3 can perform the associated action.
* `storage_class` - (Required) Class of storage used to store the object. Valid Values: `GLACIER`, `STANDARD_IA`, `ONEZONE_IA`, `INTELLIGENT_TIERING`, `DEEP_ARCHIVE`, `GLACIER_IR`.

### transition

The `transition` configuration block supports the following arguments:

* `date` - (Optional, Conflicts with `days`) Date objects are transitioned to the specified storage class. The date value must be in [RFC3339 full-date format](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) e.g. `2023-08-22`.
* `days` - (Optional, Conflicts with `date`) Number of days after creation when objects are transitioned to the specified storage class. The value must be a positive integer. If both `days` and `date` are not specified, defaults to `0`. Valid values depend on `storage_class`, see [Transition objects using Amazon S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-transition-general-considerations.html) for more details.
* `storage_class` - Class of storage used to store the object. Valid Values: `GLACIER`, `STANDARD_IA`, `ONEZONE_IA`, `INTELLIGENT_TIERING`, `DEEP_ARCHIVE`, `GLACIER_IR`.

### and

The `and` configuration block supports the following arguments:

* `object_size_greater_than` - (Optional) Minimum object size to which the rule applies. Value must be at least `0` if specified. Defaults to 128000 (128 KB) for all `storage_class` values unless `transition_default_minimum_object_size` specifies otherwise.
* `object_size_less_than` - (Optional) Maximum object size to which the rule applies. Value must be at least `1` if specified.
* `prefix` - (Optional) Prefix identifying one or more objects to which the rule applies.
* `tags` - (Optional) Key-value map of resource tags.
  All of these tags must exist in the object's tag set in order for the rule to apply.
  If set, must contain at least one key-value pair.

### tag

The `tag` configuration block supports the following arguments:

* `key` - (Required) Name of the object key.
* `value` - (Required) Value of the tag.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket` or `bucket` and `expected_bucket_owner` separated by a comma (`,`) if the latter is provided.

## Import

```bash
ytofu import aws_s3_bucket_lifecycle_configuration.example bucket-name
```
