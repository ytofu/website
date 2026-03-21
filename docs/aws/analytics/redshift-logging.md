# Resource: aws_redshift_logging

ytofu resource for managing an AWS Redshift Logging configuration.

## Basic Example

```yaml
resource:
  aws_redshift_logging:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      log_destination_type: cloudwatch
      log_exports: 
        - connectionlog
        - userlog
```

## S3 Destination Type

```yaml
resource:
  aws_redshift_logging:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      log_destination_type: s3
      bucket_name: ${aws_s3_bucket.example.id}
      s3_key_prefix: example-prefix/
```

## Argument Reference

The following arguments are required:

* `cluster_identifier` - (Required) Identifier of the source cluster.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket_name` - (Optional) Name of an existing S3 bucket where the log files are to be stored. Required when `log_destination_type` is `s3`. Must be in the same region as the cluster and the cluster must have read bucket and put object permissions. For more information on the permissions required for the bucket, please read the AWS [documentation](http://docs.aws.amazon.com/redshift/latest/mgmt/db-auditing.html#db-auditing-enable-logging)
* `log_destination_type` - (Optional) Log destination type. Valid values are `s3` and `cloudwatch`.
* `log_exports` - (Optional) Collection of exported log types. Required when `log_destination_type` is `cloudwatch`. Valid values are `connectionlog`, `useractivitylog`, and `userlog`.
* `s3_key_prefix` - (Optional) Prefix applied to the log file names.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

## Import

```bash
ytofu import aws_redshift_logging.example cluster-id-12345678
```
