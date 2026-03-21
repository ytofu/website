# Datasync Location S3

Manage Datasync Location S3 resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datasync_location_s3:
    example:
      s3_bucket_arn: ${aws_s3_bucket.example.arn}
      subdirectory: /example/prefix
      s3_config:
        bucket_access_role_arn: ${aws_iam_role.example.arn}
```

## S3 Bucket on AWS Outposts

```yaml
resource:
  aws_datasync_location_s3:
    destination:
      agent_arns: 
        - ${aws_datasync_agent.example.arn}
      s3_bucket_arn: ${aws_s3_access_point.example.arn}
      s3_storage_class: OUTPOSTS
      subdirectory: /example/prefix
      s3_config:
        bucket_access_role_arn: ${aws_iam_role.example.arn}
```
