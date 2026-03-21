# Resource: aws_s3_bucket_cors_configuration

Provides an S3 bucket CORS configuration resource. For more information about CORS, go to [Enabling Cross-Origin Resource Sharing](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html) in the Amazon S3 User Guide.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: mybucket

  aws_s3_bucket_cors_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      cors_rule:
        allowed_headers: 
          - "*"
        allowed_methods: 
          - PUT
          - POST
        allowed_origins: 
          - "https://s3-website-test.hashicorp.com"
        expose_headers: 
          - ETag
        max_age_seconds: 3000
      cors_rule:
        allowed_methods: 
          - GET
        allowed_origins: 
          - "*"```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required, Forces new resource) Name of the bucket.
* `expected_bucket_owner` - (Optional, Forces new resource, **Deprecated:**) Account ID of the expected bucket owner.
* `cors_rule` - (Required) Set of origins and methods (cross-origin access that you want to allow). [See below](#cors_rule). You can configure up to 100 rules.

### cors_rule

The `cors_rule` configuration block supports the following arguments:

* `allowed_headers` - (Optional) Set of Headers that are specified in the `Access-Control-Request-Headers` header.
* `allowed_methods` - (Required) Set of HTTP methods that you allow the origin to execute. Valid values are `GET`, `PUT`, `HEAD`, `POST`, and `DELETE`.
* `allowed_origins` - (Required) Set of origins you want customers to be able to access the bucket from.
* `expose_headers` - (Optional) Set of headers in the response that you want customers to be able to access from their applications (for example, from a JavaScript `XMLHttpRequest` object).
* `id` - (Optional) Unique identifier for the rule. The value cannot be longer than 255 characters.
* `max_age_seconds` - (Optional) Time in seconds that your browser is to cache the preflight response for the specified resource.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `bucket` or `bucket` and `expected_bucket_owner` separated by a comma (`,`) if the latter is provided.

## Import

```bash
ytofu import aws_s3_bucket_cors_configuration.example bucket-name
```
