# EKS Addon

Manage EKS Addon resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_addon:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      addon_name: vpc-cni
```
