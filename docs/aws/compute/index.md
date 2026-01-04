# AWS Compute

Manage AWS compute resources with ytofu YAML.

## Overview

AWS provides various compute services for different workloads:

| Service | Use Case |
|---------|----------|
| [EC2](ec2-instance.md) | Virtual machines with full control |
| [Lambda](lambda.md) | Serverless functions |
| [ECS](ecs.md) | Container orchestration |
| [EKS](eks.md) | Managed Kubernetes |

## Quick Start

### Launch an EC2 Instance

```yaml
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
      tags:
        Name: web-server
```

### Create a Lambda Function

```yaml
resource:
  aws_lambda_function:
    hello:
      function_name: hello-world
      runtime: python3.11
      handler: index.handler
      filename: lambda.zip
      role: ${aws_iam_role.lambda.arn}
```

### Deploy an ECS Service

```yaml
resource:
  aws_ecs_cluster:
    main:
      name: my-cluster

  aws_ecs_service:
    app:
      name: my-app
      cluster: ${aws_ecs_cluster.main.id}
      task_definition: ${aws_ecs_task_definition.app.arn}
      desired_count: 2
```

## Choosing the Right Compute Service

| Requirement | Recommended Service |
|-------------|---------------------|
| Full OS control | EC2 |
| Event-driven, short tasks | Lambda |
| Containerized apps | ECS or EKS |
| Kubernetes workloads | EKS |
| Batch processing | EC2 Spot or Lambda |

## Related Resources

- [Auto Scaling](autoscaling.md) - Scale EC2 instances automatically
- [Launch Templates](launch-template.md) - Reusable instance configurations
