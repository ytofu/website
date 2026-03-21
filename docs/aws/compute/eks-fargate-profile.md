# Resource: aws_eks_fargate_profile

Manages an EKS Fargate Profile.

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

  aws_iam_role_policy_attachment:
    example-AmazonEKSFargatePodExecutionRolePolicy:
      policy_arn: "arn:aws:iam::aws:policy/AmazonEKSFargatePodExecutionRolePolicy"
      role: ${aws_iam_role.example.name}```

## Argument Reference

The following arguments are required:

* `cluster_name` - (Required) Name of the EKS Cluster.
* `fargate_profile_name` - (Required) Name of the EKS Fargate Profile.
* `pod_execution_role_arn` - (Required) Amazon Resource Name (ARN) of the IAM Role that provides permissions for the EKS Fargate Profile.
* `selector` - (Required) Configuration block(s) for selecting Kubernetes Pods to execute with this EKS Fargate Profile. Detailed below.
* `subnet_ids` - (Required) Identifiers of private EC2 Subnets to associate with the EKS Fargate Profile. These subnets must have the following resource tag: `kubernetes.io/cluster/CLUSTER_NAME` (where `CLUSTER_NAME` is replaced with the name of the EKS Cluster).

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### selector Configuration Block

The following arguments are required:

* `namespace` - (Required) Kubernetes namespace for selection.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `labels` - (Optional) Key-value map of Kubernetes labels for selection.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the EKS Fargate Profile.
* `id` - EKS Cluster name and EKS Fargate Profile name separated by a colon (`:`).
* `status` - Status of the EKS Fargate Profile.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_eks_fargate_profile.my_fargate_profile my_cluster:my_fargate_profile
```
