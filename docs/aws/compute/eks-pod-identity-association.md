# EKS Pod Identity Association

Manage EKS Pod Identity Association resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - pods.eks.amazonaws.com
        actions:
          - "sts:AssumeRole"
          - "sts:TagSession"

resource:
  aws_iam_role:
    example:
      name: eks-pod-identity-example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    example_s3:
      policy_arn: "arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess"
      role: ${aws_iam_role.example.name}

resource:
  aws_eks_pod_identity_association:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      namespace: example
      service_account: example-sa
      role_arn: ${aws_iam_role.example.arn}
```
