# Batch Job Definition

Manage Batch Job Definition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_batch_job_definition:
    test:
      name: tf_test_batch_job_definition
      type: container
      container_properties: '{ "command": ["ls", "-la"], "image": "busybox" "resourceRequirements": [ { "type": "VCPU" "value": "0.25" }, { "type": "MEMORY" "value": "512" } ] "volumes": [ { "host": { "sourcePath": "/tmp" } "name": "tmp" } ] "environment": [ { "name": "VARNAME" "value": "VARVAL" } ] "mountPoints": [ { "sourceVolume": "tmp" "containerPath": "/tmp" "readOnly": false } ] "ulimits": [ { "hardLimit": 1024 "name": "nofile" "softLimit": 1024 } ] }'
```

## Job definition of type multinode

```yaml
resource:
  aws_batch_job_definition:
    test:
      name: tf_test_batch_job_definition_multinode
      type: multinode
      node_properties: '{ "mainNode": 0 "nodeRangeProperties": [ { "container": { "command": ["ls", "-la"] "image": "busybox" "memory": 128 "vcpus": 1 } "targetNodes": "0:" }, { "container": { "command": ["echo", "test"] "image": "busybox" "memory": 128 "vcpus": 1 } "targetNodes": "1:" } ] "numNodes": 2 }'
```

## Job Definition of type EKS

```yaml
resource:
  aws_batch_job_definition:
    test:
      name:  tf_test_batch_job_definition_eks
      type: container
      eks_properties:
        pod_properties:
          host_network: true
          containers:
            image: "public.ecr.aws/amazonlinux/amazonlinux:1"
            command:
              - sleep
              - 60
            resources:
              limits:
                cpu: 1
                memory: 1024Mi
          metadata:
            labels:
              environment: test
```

## Fargate Platform Capability

```yaml
resource:
  aws_iam_role:
    ecs_task_execution_role:
      name: tf_test_batch_exec_role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role_policy.json}

data:
  aws_iam_policy_document:
    assume_role_policy:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - ecs-tasks.amazonaws.com

resource:
  aws_iam_role_policy_attachment:
    ecs_task_execution_role_policy:
      role: ${aws_iam_role.ecs_task_execution_role.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy"

resource:
  aws_batch_job_definition:
    test:
      name: tf_test_batch_job_definition
      type: container
      platform_capabilities:
        - FARGATE
      container_properties: '{ "command": ["echo", "test"] "image": "busybox" "jobRoleArn": "arn:aws:iam::123456789012:role/AWSBatchS3ReadOnly" "fargatePlatformConfiguration": { "platformVersion": "LATEST" } "resourceRequirements": [ { "type": "VCPU" "value": "0.25" }, { "type": "MEMORY" "value": "512" } ] "executionRoleArn": aws_iam_role.ecs_task_execution_role.arn }'
```

## Job definition of type container using `ecs_properties`

```yaml
resource:
  aws_batch_job_definition:
    test:
      name: tf_test_batch_job_definition
      type: container
      platform_capabilities: 
        - FARGATE
      ecs_properties: '{ "taskProperties": [ { "executionRoleArn": aws_iam_role.ecs_task_execution_role.arn "containers": [ { "image": "public.ecr.aws/amazonlinux/amazonlinux:1" "command": ["sleep", "60"] "dependsOn": [ { "containerName": "container_b" "condition": "COMPLETE" } ] "secrets": [ { "name": "TEST" "valueFrom": "DUMMY" } ] "environment": [ { "name": "test" "value": "Environment Variable" } ] "essential": true "logConfiguration": { "logDriver": "awslogs" "options": { "awslogs-group" = "tf_test_batch_job" "awslogs-region" = "us-west-2" "awslogs-stream-prefix" = "ecs" } } "name": "container_a" "privileged": false "readonlyRootFilesystem": false "resourceRequirements": [ { "value": "1.0" "type": "VCPU" }, { "value": "2048" "type": "MEMORY" } ] }, { "image": "public.ecr.aws/amazonlinux/amazonlinux:1" "command": ["sleep", "360"] "name": "container_b" "essential": false "resourceRequirements": [ { "value": "1.0" "type": "VCPU" }, { "value": "2048" "type": "MEMORY" } ] } ] } ] }'
```
