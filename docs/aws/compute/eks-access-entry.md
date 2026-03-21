# EKS Access Entry

Manage EKS Access Entry resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_access_entry:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      principal_arn: ${aws_iam_role.example.arn}
      kubernetes_groups: 
        - group-1
        - group-2
      type: STANDARD
```
