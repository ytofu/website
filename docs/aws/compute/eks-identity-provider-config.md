# EKS Identity Provider Config

Manage EKS Identity Provider Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_identity_provider_config:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      oidc:
        client_id: your client_id
        identity_provider_config_name: example
        issuer_url: your issuer_url
```
