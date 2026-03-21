# S3 Bucket Lifecycle Configuration

Manage S3 Bucket Lifecycle Configuration resources using ytofu YAML.

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
