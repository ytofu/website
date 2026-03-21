# EMR Managed Scaling Policy

Manage EMR Managed Scaling Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emr_cluster:
    sample:
      name: emr-sample-cluster
      release_label: emr-5.30.0
      master_instance_group:
        instance_type: m4.large
      core_instance_group:
        instance_type: c4.large

resource:
  aws_emr_managed_scaling_policy:
    samplepolicy:
      cluster_id: ${aws_emr_cluster.sample.id}
      compute_limits:
        unit_type: Instances
        minimum_capacity_units: 2
        maximum_capacity_units: 10
        maximum_ondemand_capacity_units: 2
        maximum_core_capacity_units: 10
```
