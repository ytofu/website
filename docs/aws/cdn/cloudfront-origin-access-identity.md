# Resource: aws_cloudfront_origin_access_identity

Creates an Amazon CloudFront origin access identity.

## Basic Example

```yaml
resource:
  aws_cloudfront_origin_access_identity:
    example:
      comment: Some comment
```

## Argument Reference

This resource supports the following arguments:

* `comment` (Optional) - An optional comment for the origin access identity.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The origin access identity ARN.
* `caller_reference` - Internal value used by CloudFront to allow future
   updates to the origin access identity.
* `cloudfront_access_identity_path` - A shortcut to the full path for the
   origin access identity to use in CloudFront, see below.
* `etag` - The current version of the origin access identity's information.
   For example: `E2QWRUHAPOMQZL`.
* `iam_arn` - A pre-generated ARN for use in S3 bucket policies (see below).
   Example: `arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity
   E2QWRUHAPOMQZL`.
* `id` - The identifier for the origin access identity.
* `s3_canonical_user_id` - The Amazon S3 canonical user ID for the origin
   access identity, which you use when giving the origin access identity read
   permission to an object in Amazon S3.

## Import

```bash
ytofu import aws_cloudfront_origin_access_identity.origin_access E74FTE3AEXAMPLE
```
