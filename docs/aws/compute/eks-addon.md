# Resource: aws_eks_addon

Manages an EKS add-on.

## Basic Example

```yaml
resource:
  aws_eks_addon:
    example:
      cluster_name: ${aws_eks_cluster.example.name}
      addon_name: vpc-cni
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `addon_name` - (Required) Name of the EKS add-on. The name must match one of
  the names returned by [describe-addon-versions](https://docs.aws.amazon.com/cli/latest/reference/eks/describe-addon-versions.html).
* `cluster_name` - (Required) Name of the EKS Cluster.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `addon_version` - (Optional) The version of the EKS add-on. The version must
  match one of the versions returned by [describe-addon-versions](https://docs.aws.amazon.com/cli/latest/reference/eks/describe-addon-versions.html).
* `configuration_values` - (Optional) custom configuration values for addons with single JSON string. This JSON string value must match the JSON schema derived from [describe-addon-configuration](https://docs.aws.amazon.com/cli/latest/reference/eks/describe-addon-configuration.html).
* `resolve_conflicts_on_create` - (Optional) How to resolve field value conflicts when migrating a self-managed add-on to an Amazon EKS add-on. Valid values are `NONE` and `OVERWRITE`. For more details see the [CreateAddon](https://docs.aws.amazon.com/eks/latest/APIReference/API_CreateAddon.html) API Documentation.
* `resolve_conflicts_on_update` - (Optional) How to resolve field value conflicts for an Amazon EKS add-on if you've changed a value from the Amazon EKS default value. Valid values are `NONE`, `OVERWRITE`, and `PRESERVE`. For more details see the [UpdateAddon](https://docs.aws.amazon.com/eks/latest/APIReference/API_UpdateAddon.html) API Documentation.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `pod_identity_association` - (Optional) Configuration block with EKS Pod Identity association settings. See [`pod_identity_association`](#pod-identity-association) below for details.
* `preserve` - (Optional) Indicates if you want to preserve the created resources when deleting the EKS add-on.
* `service_account_role_arn` - (Optional) The Amazon Resource Name (ARN) of an
  existing IAM role to bind to the add-on's service account. The role must be
  assigned the IAM permissions required by the add-on. If you don't specify
  an existing IAM role, then the add-on uses the permissions assigned to the node
  IAM role. For more information, see [Amazon EKS node IAM role](https://docs.aws.amazon.com/eks/latest/userguide/create-node-role.html)
  in the Amazon EKS User Guide.

  ~> **Note:** To specify an existing IAM role, you must have an IAM OpenID Connect (OIDC)
  provider created for your cluster. For more information, [see Enabling IAM roles
  for service accounts on your cluster](https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html)
  in the Amazon EKS User Guide.

### pod_identity_association

* `role_arn` - (Required) The Amazon Resource Name (ARN) of the IAM role to associate with the service account. The EKS Pod Identity agent manages credentials to assume this role for applications in the containers in the pods that use this service account.
* `service_account` - (Required) The name of the Kubernetes service account inside the cluster to associate the IAM credentials with.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the EKS add-on.
* `id` - EKS Cluster name and EKS Addon name separated by a colon (`:`).
* `status` - Status of the EKS add-on.
* `created_at` - Date and time in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) that the EKS add-on was created.
* `modified_at` - Date and time in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) that the EKS add-on was updated.
* `tags_all` - (Optional) Key-value map of resource tags, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `20m`)
* `update` - (Default `20m`)
* `delete` - (Default `40m`)

## Import

```bash
ytofu import aws_eks_addon.my_eks_addon my_cluster_name:my_addon_name
```
