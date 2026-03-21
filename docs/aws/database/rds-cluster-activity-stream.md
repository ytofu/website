# Resource: aws_rds_cluster_activity_stream

Manages RDS Aurora Cluster Database Activity Streams.

## Basic Example

```yaml
resource:
  aws_rds_cluster:
    default:
      cluster_identifier: aurora-cluster-demo
      availability_zones: 
        - us-west-2a
        - us-west-2b
        - us-west-2c
      database_name: mydb
      master_username: foo
      master_password: mustbeeightcharaters
      engine: aurora-postgresql
      engine_version: 13.4

resource:
  aws_rds_cluster_instance:
    default:
      identifier: aurora-instance-demo
      cluster_identifier: ${aws_rds_cluster.default.cluster_identifier}
      engine: ${aws_rds_cluster.default.engine}
      instance_class: db.r6g.large

resource:
  aws_kms_key:
    default:
      description: AWS KMS Key to encrypt Database Activity Stream

resource:
  aws_rds_cluster_activity_stream:
    default:
      resource_arn: ${aws_rds_cluster.default.arn}
      mode: async
      kms_key_id: ${aws_kms_key.default.key_id}
      depends_on: 
        - ${aws_rds_cluster_instance.default}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required, Forces new resources) The Amazon Resource Name (ARN) of the DB cluster.
* `mode` - (Required, Forces new resources) Specifies the mode of the database activity stream. Database events such as a change or access generate an activity stream event. The database session can handle these events either synchronously or asynchronously. One of: `sync`, `async`.
* `kms_key_id` - (Required, Forces new resources) The AWS KMS key identifier for encrypting messages in the database activity stream. The AWS KMS key identifier is the key ARN, key ID, alias ARN, or alias name for the KMS key.
* `engine_native_audit_fields_included` - (Optional, Forces new resources) Specifies whether the database activity stream includes engine-native audit fields. This option only applies to an Oracle DB instance. By default, no engine-native audit fields are included. Defaults `false`.

For more detailed documentation about each argument, refer to
the [AWS official documentation][3].

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Resource Name (ARN) of the DB cluster.
* `kinesis_stream_name` - The name of the Amazon Kinesis data stream to be used for the database activity stream.

## Import

```bash
ytofu import aws_rds_cluster_activity_stream.default arn:aws:rds:us-west-2:123456789012:cluster:aurora-cluster-demo
```
