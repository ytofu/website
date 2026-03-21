# Autoscaling Group Tag

Manage Autoscaling Group Tag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_eks_node_group:
    example:
      cluster_name: example
      node_group_name: example

resource:
  aws_autoscaling_group_tag:
    example:
      autoscaling_group_name: example-value
      tag:
        key: k8s.io/cluster-autoscaler/node-template/label/eks.amazonaws.com/capacityType
        value: SPOT
        propagate_at_launch: false
```
