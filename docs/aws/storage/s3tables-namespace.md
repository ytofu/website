# Resource: aws_s3tables_namespace

ytofu resource for managing an Amazon S3 Tables Namespace.

## Basic Example

```yaml
resource:
  aws_s3tables_namespace:
    example:
      namespace: example_namespace
      table_bucket_arn: ${aws_s3tables_table_bucket.example.arn}

resource:
  aws_s3tables_table_bucket:
    example:
      name: example-bucket
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `namespace` - (Required, Forces new resource) Name of the namespace.
  Must be between 1 and 255 characters in length.
  Can consist of lowercase letters, numbers, and underscores, and must begin and end with a lowercase letter or number.
* `table_bucket_arn` - (Required, Forces new resource) ARN referencing the Table Bucket that contains this Namespace.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `created_at` - Date and time when the namespace was created.
* `created_by` - Account ID of the account that created the namespace.
* `owner_account_id` - Account ID of the account that owns the namespace.

## Import

```bash
ytofu import aws_s3tables_namespace.example 'arn:aws:s3tables:us-west-2:123456789012:bucket/example-bucket;example-namespace'
```
