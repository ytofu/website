# EKS Cluster

Manage EKS Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_cluster:
    example:
      name: example
      access_config:
        authentication_mode: API
      role_arn: ${aws_iam_role.cluster.arn}
      version: 1.31
      vpc_config:
        subnet_ids:
          - ${aws_subnet.az1.id}
          - ${aws_subnet.az2.id}
          - ${aws_subnet.az3.id}
      depends_on:
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSClusterPolicy}

resource:
  aws_iam_role:
    cluster:
      name: eks-cluster-example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "sts:AssumeRole", "sts:TagSession" ] "Effect": "Allow" "Principal": { "Service": "eks.amazonaws.com" } }, ] }'

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSClusterPolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
      role: ${aws_iam_role.cluster.name}
```

## EKS Cluster with EKS Auto Mode

```yaml
resource:
  aws_eks_cluster:
    example:
      name: example
      access_config:
        authentication_mode: API
      role_arn: ${aws_iam_role.cluster.arn}
      version: 1.31
      bootstrap_self_managed_addons: false
      compute_config:
        enabled: true
        node_pools: 
          - general-purpose
        node_role_arn: ${aws_iam_role.node.arn}
      kubernetes_network_config:
        elastic_load_balancing:
          enabled: true
      storage_config:
        block_storage:
          enabled: true
      vpc_config:
        endpoint_private_access: true
        endpoint_public_access: true
        subnet_ids:
          - ${aws_subnet.az1.id}
          - ${aws_subnet.az2.id}
          - ${aws_subnet.az3.id}
      depends_on:
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSClusterPolicy}
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSComputePolicy}
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSBlockStoragePolicy}
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSLoadBalancingPolicy}
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSNetworkingPolicy}

resource:
  aws_iam_role:
    node:
      name: eks-auto-node-example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["sts:AssumeRole"] "Effect": "Allow" "Principal": { "Service": "ec2.amazonaws.com" } }, ] }'

resource:
  aws_iam_role_policy_attachment:
    node_AmazonEKSWorkerNodeMinimalPolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSWorkerNodeMinimalPolicy"
      role: ${aws_iam_role.node.name}

resource:
  aws_iam_role_policy_attachment:
    node_AmazonEC2ContainerRegistryPullOnly:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryPullOnly"
      role: ${aws_iam_role.node.name}

resource:
  aws_iam_role:
    cluster:
      name: eks-cluster-example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "sts:AssumeRole", "sts:TagSession" ] "Effect": "Allow" "Principal": { "Service": "eks.amazonaws.com" } }, ] }'

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSClusterPolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
      role: ${aws_iam_role.cluster.name}

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSComputePolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSComputePolicy"
      role: ${aws_iam_role.cluster.name}

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSBlockStoragePolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSBlockStoragePolicy"
      role: ${aws_iam_role.cluster.name}

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSLoadBalancingPolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSLoadBalancingPolicy"
      role: ${aws_iam_role.cluster.name}

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSNetworkingPolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSNetworkingPolicy"
      role: ${aws_iam_role.cluster.name}
```

## EKS Cluster with EKS Hybrid Nodes

```yaml
resource:
  aws_eks_cluster:
    example:
      name: example
      access_config:
        authentication_mode: API
      role_arn: ${aws_iam_role.cluster.arn}
      version: 1.31
      remote_network_config:
        remote_node_networks:
          cidrs: 
            - 172.16.0.0/18
        remote_pod_networks:
          cidrs: 
            - 172.16.64.0/18
      vpc_config:
        endpoint_private_access: true
        endpoint_public_access: true
        subnet_ids:
          - ${aws_subnet.az1.id}
          - ${aws_subnet.az2.id}
          - ${aws_subnet.az3.id}
      depends_on:
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSClusterPolicy}

resource:
  aws_iam_role:
    cluster:
      name: eks-cluster-example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "sts:AssumeRole", "sts:TagSession" ] "Effect": "Allow" "Principal": { "Service": "eks.amazonaws.com" } }, ] }'

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSClusterPolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
      role: ${aws_iam_role.cluster.name}
```

## Local EKS Cluster on AWS Outpost

```yaml
resource:
  aws_eks_cluster:
    example:
      name: example
      access_config:
        authentication_mode: CONFIG_MAP
      role_arn: ${aws_iam_role.cluster.arn}
      version: 1.31
      vpc_config:
        endpoint_private_access: true
        endpoint_public_access: false
        subnet_ids:
          - ${aws_subnet.az1.id}
          - ${aws_subnet.az2.id}
          - ${aws_subnet.az3.id}
      outpost_config:
        control_plane_instance_type: m5.large
        outpost_arns: 
          - ${data.aws_outposts_outpost.example.arn}
      depends_on:
        - ${aws_iam_role_policy_attachment.cluster_AmazonEKSLocalOutpostClusterPolicy}

data:
  aws_outposts_outpost:
    example:
      name: example

resource:
  aws_iam_role:
    cluster:
      name: eks-cluster-example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "sts:AssumeRole", "sts:TagSession" ] "Effect": "Allow" "Principal": { "Service": [ "eks.amazonaws.com", "ec2.amazonaws.com" ] } }, ] }'

resource:
  aws_iam_role_policy_attachment:
    cluster_AmazonEKSLocalOutpostClusterPolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSLocalOutpostClusterPolicy"
      role: ${aws_iam_role.cluster.name}
```
