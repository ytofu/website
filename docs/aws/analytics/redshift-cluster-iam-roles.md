# Resource: aws_redshift_cluster_iam_roles

Provides a Redshift Cluster IAM Roles resource.

## Basic Example

```yaml
resource:
  aws_redshift_cluster_iam_roles:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.cluster_identifier}
      iam_role_arns: 
        - ${aws_iam_role.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cluster_identifier` - (Required) The name of the Redshift Cluster IAM Roles.
* `iam_role_arns` - (Optional) A list of IAM Role ARNs to associate with the cluster. A Maximum of 10 can be associated to the cluster at any time.
* `default_iam_role_arn` - (Optional) The Amazon Resource Name (ARN) for the IAM role that was set as default for the cluster when the cluster was created.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Redshift Cluster ID.

## Import

```bash
ytofu import aws_redshift_cluster_iam_roles.examplegroup1 example
```
