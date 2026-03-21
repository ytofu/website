# Resource: aws_db_instance_automated_backups_replication

Manage cross-region replication of automated backups to a different AWS Region. Documentation for cross-region automated backup replication can be found at:

## Basic Example

```yaml
resource:
  aws_db_instance_automated_backups_replication:
    default:
      source_db_instance_arn: "arn:aws:rds:us-west-2:123456789012:db:mydatabase"
      retention_period: 14
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `kms_key_id` - (Optional, Forces new resource) The AWS KMS key identifier for encryption of the replicated automated backups. The KMS key ID is the Amazon Resource Name (ARN) for the KMS encryption key in the destination AWS Region, for example, `arn:aws:kms:us-east-1:123456789012:key/AKIAIOSFODNN7EXAMPLE`.
* `pre_signed_url` - (Optional, Forces new resource) A URL that contains a [Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html) signed request for the [`StartDBInstanceAutomatedBackupsReplication`](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_StartDBInstanceAutomatedBackupsReplication.html) action to be called in the AWS Region of the source DB instance.
* `retention_period` - (Optional, Forces new resource) The retention period for the replicated automated backups, defaults to `7`.
* `source_db_instance_arn` - (Required, Forces new resource) The Amazon Resource Name (ARN) of the source DB instance for the replicated automated backups, for example, `arn:aws:rds:us-west-2:123456789012:db:mydatabase`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Resource Name (ARN) of the replicated automated backups.

## Timeouts

Configuration options:

- `create` - (Default `75m`)
- `delete` - (Default `75m`)

## Import

```bash
ytofu import aws_db_instance_automated_backups_replication.default arn:aws:rds:us-east-1:123456789012:auto-backup:ab-faaa2mgdj1vmp4xflr7yhsrmtbtob7ltrzzz2my
```
