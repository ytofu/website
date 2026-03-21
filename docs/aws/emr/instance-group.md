# EMR Instance Group

Add instance groups to EMR clusters using ytofu YAML.

## Task Instance Group

```yaml
resource:
  aws_emr_instance_group:
    task:
      cluster_id: ${aws_emr_cluster.example.id}
      instance_count: 1
      instance_type: m5.xlarge
      name: task-group
```

## With EBS Configuration

```yaml
resource:
  aws_emr_instance_group:
    task:
      cluster_id: ${aws_emr_cluster.example.id}
      instance_count: 2
      instance_type: m5.xlarge
      name: task-group
      ebs_config:
        - size: 100
          type: gp3
          volumes_per_instance: 1
```
