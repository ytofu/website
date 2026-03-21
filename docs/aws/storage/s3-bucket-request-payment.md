# S3 Bucket Request Payment

Configure requester-pays settings for S3 buckets using ytofu YAML.

## Requester Pays

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

  aws_s3_bucket_request_payment_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      payer: Requester
```

## Bucket Owner Pays (Default)

```yaml
resource:
  aws_s3_bucket_request_payment_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      payer: BucketOwner
```
