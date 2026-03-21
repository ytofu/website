# EMR Cluster

Create EMR clusters using ytofu YAML.

## Basic Spark Cluster

```yaml
resource:
  aws_emr_cluster:
    example:
      name: emr-spark-cluster
      release_label: emr-6.15.0
      applications:
        - Spark
        - Hive
      service_role: ${aws_iam_role.emr.arn}
      ec2_attributes:
        instance_profile: ${aws_iam_instance_profile.emr.arn}
        subnet_id: ${aws_subnet.example.id}
        emr_managed_master_security_group: ${aws_security_group.master.id}
        emr_managed_slave_security_group: ${aws_security_group.slave.id}
      master_instance_group:
        instance_type: m5.xlarge
      core_instance_group:
        instance_type: m5.xlarge
        instance_count: 2
      tags:
        Role: EMR_DefaultRole
        Environment: production
```

## With Auto-Termination

```yaml
resource:
  aws_emr_cluster:
    example:
      name: emr-auto-terminate
      release_label: emr-6.15.0
      applications:
        - Spark
      service_role: ${aws_iam_role.emr.arn}
      auto_termination_policy:
        idle_timeout: 3600
      ec2_attributes:
        instance_profile: ${aws_iam_instance_profile.emr.arn}
        subnet_id: ${aws_subnet.example.id}
      master_instance_group:
        instance_type: m5.xlarge
      core_instance_group:
        instance_type: m5.xlarge
        instance_count: 1
```

## With Bootstrap Actions

```yaml
resource:
  aws_emr_cluster:
    example:
      name: emr-with-bootstrap
      release_label: emr-6.15.0
      applications:
        - Spark
      service_role: ${aws_iam_role.emr.arn}
      ec2_attributes:
        instance_profile: ${aws_iam_instance_profile.emr.arn}
        subnet_id: ${aws_subnet.example.id}
      master_instance_group:
        instance_type: m5.xlarge
      core_instance_group:
        instance_type: m5.xlarge
        instance_count: 2
      bootstrap_action:
        - path: s3://my-bucket/scripts/bootstrap.sh
          name: install-deps
          args:
            - --option1
            - value1
      step:
        - action_on_failure: TERMINATE_CLUSTER
          hadoop_jar_step:
            jar: command-runner.jar
            args:
              - spark-submit
              - s3://my-bucket/jobs/etl.py
          name: Run ETL
```
