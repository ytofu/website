# RDS Cluster Activity Stream

Manage RDS Cluster Activity Stream resources using ytofu YAML.

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
