# EKS Capability

Manage EKS Capability resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_capability:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      capability_name: argocd
      type: ARGOCD
      role_arn: ${aws_iam_role.example.arn}
      delete_propagation_policy: RETAIN
      configuration:
        argo_cd:
          aws_idc:
            idc_instance_arn: "arn:aws:sso:::instance/ssoins-1234567890abcdef0"
          namespace: argocd
      tags:
        Name: example-capability
```
