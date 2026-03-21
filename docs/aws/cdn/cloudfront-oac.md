# CloudFront Origin Access Control

Configure origin access control for S3 origins using ytofu YAML.

## S3 Origin

```yaml
resource:
  aws_cloudfront_origin_access_control:
    default:
      name: default-oac
      description: Default OAC for S3
      origin_access_control_origin_type: s3
      signing_behavior: always
      signing_protocol: sigv4
```

## Lambda Function URL Origin

```yaml
resource:
  aws_cloudfront_origin_access_control:
    lambda:
      name: lambda-oac
      origin_access_control_origin_type: lambda
      signing_behavior: always
      signing_protocol: sigv4
```
