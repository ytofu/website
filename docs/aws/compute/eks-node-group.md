# EKS Node Group

Manage EKS Node Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_node_group:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      node_group_name: example
      node_role_arn: ${aws_iam_role.example.arn}
      subnet_ids: ${aws_subnet.example[*].id}
      scaling_config:
        desired_size: 1
        max_size: 2
        min_size: 1
      update_config:
        max_unavailable: 1
      depends_on:
        - ${aws_iam_role_policy_attachment.example-AmazonEKSWorkerNodePolicy}
        - ${aws_iam_role_policy_attachment.example-AmazonEKS_CNI_Policy}
        - ${aws_iam_role_policy_attachment.example-AmazonEC2ContainerRegistryReadOnly}
```

## Ignoring Changes to Desired Size

```yaml
resource:
  aws_eks_node_group:
    example:
      scaling_config:
        desired_size: 2
      lifecycle:
        ignore_changes: 
          - ${scaling_config[0].desired_size}
```

## Tracking the latest EKS Node Group AMI releases

```yaml
data:
  aws_ssm_parameter:
    eks_ami_release_version:
      name: "/aws/service/eks/optimized-ami/${aws_eks_cluster.example.version}/amazon-linux-2023/x86_64/standard/recommended/release_version"

resource:
  aws_eks_node_group:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      node_group_name: example
      version: ${aws_eks_cluster.example.version}
      release_version: value
      node_role_arn: ${aws_iam_role.example.arn}
      subnet_ids: ${aws_subnet.example[*].id}
```

## Example IAM Role for EKS Node Group

```yaml
resource:
  aws_iam_role:
    example:
      name: eks-node-group-example
      assume_role_policy: '{ "Statement": [{ "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "ec2.amazonaws.com" } }] "Version": "2012-10-17" }'

resource:
  aws_iam_role_policy_attachment:
    example-AmazonEKSWorkerNodePolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy"
      role: ${aws_iam_role.example.name}

resource:
  aws_iam_role_policy_attachment:
    example-AmazonEKS_CNI_Policy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy"
      role: ${aws_iam_role.example.name}

resource:
  aws_iam_role_policy_attachment:
    example-AmazonEC2ContainerRegistryReadOnly:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"
      role: ${aws_iam_role.example.name}
```

## Example Subnets for EKS Node Group

```yaml
data:
  aws_availability_zones:
    available:
      state: available

resource:
  aws_subnet:
    example:
      availability_zone: ${data.aws_availability_zones.available.names[count.index]}
      cidr_block: 10.0.1.0/24
      vpc_id: ${aws_vpc.example.id}
```
