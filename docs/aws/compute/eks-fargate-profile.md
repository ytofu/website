# EKS Fargate Profile

Manage EKS Fargate Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_fargate_profile:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      fargate_profile_name: example
      pod_execution_role_arn: ${aws_iam_role.example.arn}
      subnet_ids: ${aws_subnet.example[*].id}
      selector:
        namespace: example
```

## Example IAM Role for EKS Fargate Profile

```yaml
resource:
  aws_iam_role:
    example:
      name: eks-fargate-profile-example
      assume_role_policy: '{ "Statement": [{ "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "eks-fargate-pods.amazonaws.com" } }] "Version": "2012-10-17" }'

resource:
  aws_iam_role_policy_attachment:
    example-AmazonEKSFargatePodExecutionRolePolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSFargatePodExecutionRolePolicy"
      role: ${aws_iam_role.example.name}
```
