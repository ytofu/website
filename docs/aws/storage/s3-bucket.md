# S3 Bucket

Manage S3 Bucket resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-test-bucket
      tags:
        Name: My bucket
        Environment: Dev
```

## Bucket In Account-Regional Namespace

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_region:
    current:

resource:
  aws_s3_bucket:
    example:
      bucket: example-formatted
      bucket_namespace: account-regional
```
