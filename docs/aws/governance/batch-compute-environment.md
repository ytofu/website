# Batch Compute Environment

Manage Batch Compute Environment resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    ec2_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - ec2.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    ecs_instance_role:
      name: ecs_instance_role
      assume_role_policy: ${data.aws_iam_policy_document.ec2_assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    ecs_instance_role:
      role: ${aws_iam_role.ecs_instance_role.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AmazonEC2ContainerServiceforEC2Role"

resource:
  aws_iam_instance_profile:
    ecs_instance_role:
      name: ecs_instance_role
      role: ${aws_iam_role.ecs_instance_role.name}

data:
  aws_iam_policy_document:
    batch_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - batch.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    aws_batch_service_role:
      name: aws_batch_service_role
      assume_role_policy: ${data.aws_iam_policy_document.batch_assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    aws_batch_service_role:
      role: ${aws_iam_role.aws_batch_service_role.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSBatchServiceRole"

resource:
  aws_security_group:
    sample:
      name: aws_batch_compute_environment_security_group
      egress:
        from_port: 0
        to_port: 0
        protocol: -1
        cidr_blocks: 
          - 0.0.0.0/0

resource:
  aws_vpc:
    sample:
      cidr_block: 10.1.0.0/16

resource:
  aws_subnet:
    sample:
      vpc_id: ${aws_vpc.sample.id}
      cidr_block: 10.1.1.0/24

resource:
  aws_placement_group:
    sample:
      name: sample
      strategy: cluster

resource:
  aws_batch_compute_environment:
    sample:
      name: sample
      compute_resources:
        instance_role: ${aws_iam_instance_profile.ecs_instance_role.arn}
        instance_type:
          - c4.large
        max_vcpus: 16
        min_vcpus: 0
        placement_group: ${aws_placement_group.sample.name}
        security_group_ids:
          - ${aws_security_group.sample.id}
        subnets:
          - ${aws_subnet.sample.id}
        type: EC2
      service_role: ${aws_iam_role.aws_batch_service_role.arn}
      type: MANAGED
      depends_on: 
        - ${aws_iam_role_policy_attachment.aws_batch_service_role}
```

## Fargate Type

```yaml
resource:
  aws_batch_compute_environment:
    sample:
      name: sample
      compute_resources:
        max_vcpus: 16
        security_group_ids:
          - ${aws_security_group.sample.id}
        subnets:
          - ${aws_subnet.sample.id}
        type: FARGATE
      service_role: ${aws_iam_role.aws_batch_service_role.arn}
      type: MANAGED
      depends_on: 
        - ${aws_iam_role_policy_attachment.aws_batch_service_role}
```

## Setting Update Policy

```yaml
resource:
  aws_batch_compute_environment:
    sample:
      name: sample
      compute_resources:
        allocation_strategy: BEST_FIT_PROGRESSIVE
        instance_role: ${aws_iam_instance_profile.ecs_instance.arn}
        instance_type: 
          - optimal
        max_vcpus: 4
        min_vcpus: 0
        security_group_ids:
          - ${aws_security_group.sample.id}
        subnets:
          - ${aws_subnet.sample.id}
        type: EC2
      update_policy:
        job_execution_timeout_minutes: 30
        terminate_jobs_on_update: false
      type: MANAGED
```
