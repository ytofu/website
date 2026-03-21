# IAM OIDC Provider

Create OpenID Connect identity providers using ytofu YAML.

## EKS OIDC Provider

```yaml
data:
  tls_certificate:
    eks:
      url: ${aws_eks_cluster.example.identity[0].oidc[0].issuer}

resource:
  aws_iam_openid_connect_provider:
    eks:
      client_id_list:
        - sts.amazonaws.com
      thumbprint_list:
        - ${data.tls_certificate.eks.certificates[0].sha1_fingerprint}
      url: ${aws_eks_cluster.example.identity[0].oidc[0].issuer}
```

## GitHub Actions OIDC

```yaml
resource:
  aws_iam_openid_connect_provider:
    github:
      url: https://token.actions.githubusercontent.com
      client_id_list:
        - sts.amazonaws.com
      thumbprint_list:
        - 6938fd4d98bab03faadb97b34396831e3780aea1
```
