# RDS Cluster Role Association

Manage RDS Cluster Role Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rds_cluster_role_association:
    example:
      db_cluster_identifier: ${aws_rds_cluster.example.id}
      feature_name: S3_INTEGRATION
      role_arn: ${aws_iam_role.example.arn}
```
