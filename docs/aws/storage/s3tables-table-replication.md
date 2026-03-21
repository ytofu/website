# Resource: aws_s3tables_table_replication

Manages Amazon S3 Tables Table Replication configuration.

## Basic Example

```yaml
resource:
  aws_s3tables_table_replication:
    example:
      table_arn: ${aws_s3tables_table.example.arn}
      role: ${aws_iam_role.example.arn}
      rule:
        destination:
          destination_table_bucket_arn: ${aws_s3tables_table_bucket.target.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `role` - (Required) ARN referencing the IAM role assumed by S3 when replicating tables.
* `rule` - (Optional) Replication rules. See [Rule](#rule) below for more details.
* `table_arn` - (Required, Forces new resource) ARN referencing the Table that owns this replication configuration.

### Rule

The `rule` block supports the following:

* `destination` - (Required) Replication destination. See [Destination](#destination) below for more details.

### Destination

The `destination` block supports the following:

* `destination_table_bucket_arn` (Required) ARN of destination table bucket to replicate source tables to.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_s3tables_table_replication.example 'arn:aws:s3tables:us-west-2:123456789012:table/example-table'
```
