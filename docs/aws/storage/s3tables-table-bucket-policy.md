# Resource: aws_s3tables_table_bucket_policy

ytofu resource for managing an Amazon S3 Tables Table Bucket Policy.

## Basic Example

```yaml
resource:
  aws_s3tables_table_bucket_policy:
    example:
      resource_policy: ${data.aws_iam_policy_document.example.json}
      table_bucket_arn: ${aws_s3tables_table_bucket.example.arn}

  aws_s3tables_table_bucket:
    example:
      name: example-bucket

data:
  aws_iam_policy_document:
    example:
      statement:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_policy` - (Required) Amazon Web Services resource-based policy document in JSON format.
* `table_bucket_arn` - (Required, Forces new resource) ARN referencing the Table Bucket that owns this policy.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_s3tables_table_bucket_policy.example 'arn:aws:s3tables:us-west-2:123456789012:bucket/example-bucket;example-namespace'
```
