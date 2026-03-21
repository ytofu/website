# EKS Access Policy Associattion

Manage EKS Access Policy Associattion resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_access_policy_association:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      policy_arn: "arn:aws:eks::aws:cluster-access-policy/AmazonEKSViewPolicy"
      principal_arn: ${aws_iam_user.example.arn}
      access_scope:
        type: namespace
        namespaces: 
          - example-namespace
```
