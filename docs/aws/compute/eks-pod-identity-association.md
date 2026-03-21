# Resource: aws_eks_pod_identity_association

ytofu resource for managing an AWS EKS (Elastic Kubernetes) Pod Identity Association.

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

  aws_iam_role_policy_attachment:
    example_s3:
      policy_arn: "arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess"
      role: ${aws_iam_role.example.name}

  aws_eks_pod_identity_association:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      namespace: example
      service_account: example-sa
      role_arn: ${aws_iam_role.example.arn}```

## Argument Reference

The following arguments are required:

* `cluster_name` - (Required) The name of the cluster to create the association in.
* `namespace` - (Required) The name of the Kubernetes namespace inside the cluster to create the association in. The service account and the pods that use the service account must be in this namespace.
* `role_arn` - (Required) The Amazon Resource Name (ARN) of the IAM role to associate with the service account. The EKS Pod Identity agent manages credentials to assume this role for applications in the containers in the pods that use this service account.
* `service_account` - (Required) The name of the Kubernetes service account inside the cluster to associate the IAM credentials with.

The following arguments are optional:

* `disable_session_tags` - (Optional) Disable the tags that are automatically added to role session by Amazon EKS.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `target_role_arn` - (Optional) The Amazon Resource Name (ARN) of the IAM role to be chained to the the IAM role specified as `role_arn`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `association_arn` - The Amazon Resource Name (ARN) of the association.
* `association_id` - The ID of the association.
* `external_id` - The unique identifier for this association for a target IAM role. You put this value in the trust policy of the target role, in a Condition to match the sts.ExternalId.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_eks_pod_identity_association.example example,a-12345678
```
