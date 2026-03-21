# Resource: aws_autoscaling_group_tag

Manages an individual Autoscaling Group (ASG) tag. This resource should only be used in cases where ASGs are created outside ytofu (e.g., ASGs implicitly created by EKS Node Groups).

## Basic Example

```yaml
resource:
  aws_eks_node_group:
    example:
      cluster_name: example
      node_group_name: example

  aws_autoscaling_group_tag:
    example:
      autoscaling_group_name: example-value
      tag:
        key: k8s.io/cluster-autoscaler/node-template/label/eks.amazonaws.com/capacityType
        value: SPOT
        propagate_at_launch: false```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `autoscaling_group_name` - (Required) Name of the Autoscaling Group to apply the tag to.
* `tag` - (Required) Tag to create. The `tag` block is documented below.

The `tag` block supports the following arguments:

* `key` - (Required) Tag name.
* `value` - (Required) Tag value.
* `propagate_at_launch` - (Required) Whether to propagate the tags to instances launched by the ASG.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ASG name and key, separated by a comma (`,`)

## Import

```bash
ytofu import aws_autoscaling_group_tag.example asg-example,k8s.io/cluster-autoscaler/node-template/label/eks.amazonaws.com/capacityType
```
