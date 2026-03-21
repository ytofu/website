# Resource: aws_rds_cluster_role_association

Manages a RDS DB Cluster association with an IAM Role. Example use cases:

## Basic Example

```yaml
resource:
  aws_rds_cluster_role_association:
    example:
      db_cluster_identifier: ${aws_rds_cluster.example.id}
      feature_name: S3_INTEGRATION
      role_arn: ${aws_iam_role.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `db_cluster_identifier` - (Required) DB Cluster Identifier to associate with the IAM Role.
* `feature_name` - (Optional) Name of the feature for association. This can be found in the AWS documentation relevant to the integration or a full list is available in the `SupportedFeatureNames` list returned by [AWS CLI rds describe-db-engine-versions](https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-engine-versions.html).
* `role_arn` - (Required) Amazon Resource Name (ARN) of the IAM Role to associate with the DB Cluster.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - DB Cluster Identifier and IAM Role ARN separated by a comma (`,`)

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_rds_cluster_role_association.example my-db-cluster,arn:aws:iam::123456789012:role/my-role
```
