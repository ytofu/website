# Redshift Cluster IAM Roles

Manage Redshift Cluster IAM Roles resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_cluster_iam_roles:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.cluster_identifier}
      iam_role_arns: 
        - ${aws_iam_role.example.arn}
```
