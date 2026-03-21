# Emrcontainers Virtual Cluster

Manage Emrcontainers Virtual Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emrcontainers_virtual_cluster:
    example:
      container_provider:
        id: ${aws_eks_cluster.example.name}
        type: EKS
        info:
          eks_info:
            namespace: default
      name: example
```
