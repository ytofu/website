# EKS (Elastic Kubernetes Service)

Deploy and manage Kubernetes clusters with Amazon EKS using ytofu YAML.

## Basic EKS Cluster

```yaml
resource:
  aws_eks_cluster:
    main:
      name: my-cluster
      role_arn: ${aws_iam_role.eks_cluster.arn}

      vpc_config:
        subnet_ids:
          - ${aws_subnet.private_a.id}
          - ${aws_subnet.private_b.id}

      tags:
        Name: my-cluster
```

## Complete EKS Setup

```yaml
resource:
  # EKS Cluster
  aws_eks_cluster:
    main:
      name: my-cluster
      role_arn: ${aws_iam_role.eks_cluster.arn}
      version: "1.29"

      vpc_config:
        subnet_ids:
          - ${aws_subnet.private_a.id}
          - ${aws_subnet.private_b.id}
        endpoint_private_access: true
        endpoint_public_access: true
        public_access_cidrs:
          - 0.0.0.0/0

      enabled_cluster_log_types:
        - api
        - audit
        - authenticator
        - controllerManager
        - scheduler

      tags:
        Name: my-cluster

  # Managed Node Group
  aws_eks_node_group:
    main:
      cluster_name: ${aws_eks_cluster.main.name}
      node_group_name: main
      node_role_arn: ${aws_iam_role.eks_node.arn}
      subnet_ids:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}

      scaling_config:
        desired_size: 2
        max_size: 5
        min_size: 1

      instance_types:
        - t3.medium

      update_config:
        max_unavailable: 1

      tags:
        Name: main-nodes
```

## Arguments Reference (Cluster)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | Yes | Cluster name |
| role_arn | string | Yes | Cluster IAM role ARN |
| vpc_config | object | Yes | VPC configuration |
| version | string | No | Kubernetes version |
| enabled_cluster_log_types | list | No | Control plane logs |
| encryption_config | object | No | Secrets encryption |
| tags | map | No | Resource tags |

## Arguments Reference (Node Group)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| cluster_name | string | Yes | EKS cluster name |
| node_group_name | string | Yes | Node group name |
| node_role_arn | string | Yes | Node IAM role ARN |
| subnet_ids | list | Yes | Subnet IDs |
| scaling_config | object | Yes | Scaling configuration |
| instance_types | list | No | EC2 instance types |
| ami_type | string | No | AMI type |
| capacity_type | string | No | ON_DEMAND or SPOT |
| disk_size | number | No | EBS volume size |
| labels | map | No | Kubernetes labels |
| taint | list | No | Kubernetes taints |

## Common Patterns

### IAM Roles for EKS

```yaml
resource:
  # Cluster Role
  aws_iam_role:
    eks_cluster:
      name: eks-cluster-role
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Action": "sts:AssumeRole",
            "Principal": {"Service": "eks.amazonaws.com"},
            "Effect": "Allow"
          }]
        }

  aws_iam_role_policy_attachment:
    eks_cluster:
      role: ${aws_iam_role.eks_cluster.name}
      policy_arn: arn:aws:iam::aws:policy/AmazonEKSClusterPolicy

  # Node Role
  aws_iam_role:
    eks_node:
      name: eks-node-role
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Action": "sts:AssumeRole",
            "Principal": {"Service": "ec2.amazonaws.com"},
            "Effect": "Allow"
          }]
        }

  aws_iam_role_policy_attachment:
    eks_worker:
      role: ${aws_iam_role.eks_node.name}
      policy_arn: arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy

    eks_cni:
      role: ${aws_iam_role.eks_node.name}
      policy_arn: arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy

    ecr_readonly:
      role: ${aws_iam_role.eks_node.name}
      policy_arn: arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly
```

### Fargate Profile

```yaml
resource:
  aws_eks_fargate_profile:
    default:
      cluster_name: ${aws_eks_cluster.main.name}
      fargate_profile_name: default
      pod_execution_role_arn: ${aws_iam_role.eks_fargate.arn}
      subnet_ids:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}

      selector:
        - namespace: default
        - namespace: kube-system

  aws_iam_role:
    eks_fargate:
      name: eks-fargate-role
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Action": "sts:AssumeRole",
            "Principal": {"Service": "eks-fargate-pods.amazonaws.com"},
            "Effect": "Allow"
          }]
        }

  aws_iam_role_policy_attachment:
    eks_fargate:
      role: ${aws_iam_role.eks_fargate.name}
      policy_arn: arn:aws:iam::aws:policy/AmazonEKSFargatePodExecutionRolePolicy
```

### Spot Instance Node Group

```yaml
resource:
  aws_eks_node_group:
    spot:
      cluster_name: ${aws_eks_cluster.main.name}
      node_group_name: spot
      node_role_arn: ${aws_iam_role.eks_node.arn}
      subnet_ids:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}

      capacity_type: SPOT

      instance_types:
        - t3.medium
        - t3.large
        - t3a.medium
        - t3a.large

      scaling_config:
        desired_size: 2
        max_size: 10
        min_size: 0

      labels:
        node-type: spot

      taint:
        - key: spot
          value: "true"
          effect: NO_SCHEDULE
```

### EKS Add-ons

```yaml
resource:
  aws_eks_addon:
    vpc_cni:
      cluster_name: ${aws_eks_cluster.main.name}
      addon_name: vpc-cni
      addon_version: v1.16.0-eksbuild.1
      resolve_conflicts_on_update: PRESERVE

    coredns:
      cluster_name: ${aws_eks_cluster.main.name}
      addon_name: coredns
      addon_version: v1.11.1-eksbuild.4
      resolve_conflicts_on_update: PRESERVE

    kube_proxy:
      cluster_name: ${aws_eks_cluster.main.name}
      addon_name: kube-proxy
      addon_version: v1.29.0-eksbuild.1
      resolve_conflicts_on_update: PRESERVE

    ebs_csi:
      cluster_name: ${aws_eks_cluster.main.name}
      addon_name: aws-ebs-csi-driver
      addon_version: v1.28.0-eksbuild.1
      service_account_role_arn: ${aws_iam_role.ebs_csi.arn}
```

### OIDC Provider for IRSA

```yaml
data:
  tls_certificate:
    eks:
      url: ${aws_eks_cluster.main.identity[0].oidc[0].issuer}

resource:
  aws_iam_openid_connect_provider:
    eks:
      client_id_list:
        - sts.amazonaws.com
      thumbprint_list:
        - ${data.tls_certificate.eks.certificates[0].sha1_fingerprint}
      url: ${aws_eks_cluster.main.identity[0].oidc[0].issuer}
```

### IAM Role for Service Accounts (IRSA)

```yaml
data:
  aws_caller_identity:
    current: {}

resource:
  aws_iam_role:
    app_sa:
      name: app-service-account-role
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Effect": "Allow",
            "Principal": {
              "Federated": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:oidc-provider/${replace(aws_eks_cluster.main.identity[0].oidc[0].issuer, "https://", "")}"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
              "StringEquals": {
                "${replace(aws_eks_cluster.main.identity[0].oidc[0].issuer, "https://", "")}:sub": "system:serviceaccount:default:my-app",
                "${replace(aws_eks_cluster.main.identity[0].oidc[0].issuer, "https://", "")}:aud": "sts.amazonaws.com"
              }
            }
          }]
        }
```

## Outputs

```yaml
output:
  cluster_endpoint:
    value: ${aws_eks_cluster.main.endpoint}

  cluster_ca_certificate:
    value: ${aws_eks_cluster.main.certificate_authority[0].data}

  cluster_name:
    value: ${aws_eks_cluster.main.name}
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| cluster.id | Cluster ID |
| cluster.arn | Cluster ARN |
| cluster.endpoint | API server endpoint |
| cluster.certificate_authority | CA certificate |
| cluster.identity | OIDC identity provider |
| node_group.id | Node group ID |
| node_group.arn | Node group ARN |
| node_group.status | Node group status |

## Best Practices

- **Use managed node groups** for easier management
- **Enable control plane logging** for audit
- **Use IRSA** instead of node-level IAM
- **Implement network policies** for pod security
- **Use private endpoints** when possible
- **Keep clusters updated** to latest versions
- **Use multiple AZs** for high availability
- **Consider Fargate** for serverless workloads

## Related Resources

- [VPC](../networking/vpc.md)
- [Security Groups](../networking/security-groups.md)
- [Load Balancer](../networking/load-balancer.md)
- [ECS](ecs.md)
