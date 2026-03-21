# Resource: aws_redshift_snapshot_copy_grant

Creates a snapshot copy grant that allows AWS Redshift to encrypt copied snapshots with a customer master key from AWS KMS in a destination region.

## Basic Example

```yaml
resource:
  aws_redshift_snapshot_copy_grant:
    test:
      snapshot_copy_grant_name: my-grant

  aws_redshift_cluster:
    test:
      snapshot_copy:
        destination_region: us-east-2
        grant_name: ${aws_redshift_snapshot_copy_grant.test.snapshot_copy_grant_name}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `snapshot_copy_grant_name` - (Required, Forces new resource) A friendly name for identifying the grant.
* `kms_key_id` - (Optional, Forces new resource) The unique identifier for the customer master key (CMK) that the grant applies to. Specify the key ID or the Amazon Resource Name (ARN) of the CMK. To specify a CMK in a different AWS account, you must use the key ARN. If not specified, the default key is used.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of snapshot copy grant
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_redshift_snapshot_copy_grant.test my-grant
```
