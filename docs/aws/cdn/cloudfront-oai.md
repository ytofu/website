# CloudFront Origin Access Identity

Legacy origin access identity for S3 origins using ytofu YAML.

!!! note
    For new distributions, use Origin Access Control (OAC) instead.

## Basic OAI

```yaml
resource:
  aws_cloudfront_origin_access_identity:
    example:
      comment: Access identity for S3 bucket
```
