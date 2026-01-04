# Container Deployment

Deploy a containerized application using ECS Fargate.

**Level:** Advanced
**Time:** 45-60 minutes

## What You'll Build

```
┌─────────────────────────────────────────────────────────────┐
│                      VPC (10.0.0.0/16)                      │
│  ┌────────────────────┐    ┌────────────────────┐           │
│  │  Public Subnet A   │    │  Public Subnet B   │           │
│  │   (10.0.1.0/24)    │    │   (10.0.2.0/24)    │           │
│  │                    │    │                    │           │
│  │  ┌──────────────┐  │    │  ┌──────────────┐  │           │
│  │  │ ECS Fargate  │  │    │  │ ECS Fargate  │  │           │
│  │  │   Task       │  │    │  │   Task       │  │           │
│  │  └──────────────┘  │    │  └──────────────┘  │           │
│  └─────────┬──────────┘    └───────────┬────────┘           │
│            └───────────┬───────────────┘                    │
│                        │                                    │
│                 ┌──────┴──────┐                             │
│                 │     ALB     │                             │
│                 └──────┬──────┘                             │
│                        │                                    │
│                 ┌──────┴──────┐                             │
│                 │     IGW     │                             │
│                 └──────┬──────┘                             │
└────────────────────────┼────────────────────────────────────┘
                         │
                     Internet
```

## Prerequisites

- Completed [Web Application Stack](web-app-stack.md) tutorial
- AWS credentials with ECS, ECR, and IAM permissions

## Step 1: Create Project Directory

```bash
mkdir container-deployment
cd container-deployment
```

## Step 2: Provider Configuration

Create `provider.yaml`:

```yaml
provider:
  aws:
    region: us-west-2
```

## Step 3: Create VPC Infrastructure

Create `vpc.yaml`:

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true
      tags:
        Name: ecs-vpc

  aws_subnet:
    public_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet-a

    public_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.2.0/24
      availability_zone: us-west-2b
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet-b

  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-igw

  aws_route_table:
    public:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}
      tags:
        Name: public-rt

  aws_route_table_association:
    public_a:
      subnet_id: ${aws_subnet.public_a.id}
      route_table_id: ${aws_route_table.public.id}

    public_b:
      subnet_id: ${aws_subnet.public_b.id}
      route_table_id: ${aws_route_table.public.id}
```

## Step 4: Create Security Groups

Create `security.yaml`:

```yaml
resource:
  aws_security_group:
    alb:
      name: alb-sg
      description: ALB security group
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - from_port: 80
          to_port: 80
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0

      egress:
        - from_port: 0
          to_port: 0
          protocol: "-1"
          cidr_blocks:
            - 0.0.0.0/0

      tags:
        Name: alb-sg

  aws_security_group:
    ecs:
      name: ecs-sg
      description: ECS tasks security group
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - from_port: 80
          to_port: 80
          protocol: tcp
          security_groups:
            - ${aws_security_group.alb.id}

      egress:
        - from_port: 0
          to_port: 0
          protocol: "-1"
          cidr_blocks:
            - 0.0.0.0/0

      tags:
        Name: ecs-sg
```

## Step 5: Create IAM Roles

Create `iam.yaml`:

```yaml
data:
  aws_iam_policy_document:
    ecs_assume_role:
      statement:
        - effect: Allow
          principals:
            - type: Service
              identifiers:
                - ecs-tasks.amazonaws.com
          actions:
            - sts:AssumeRole

resource:
  aws_iam_role:
    ecs_execution:
      name: ecs-execution-role
      assume_role_policy: ${data.aws_iam_policy_document.ecs_assume_role.json}
      tags:
        Name: ecs-execution-role

    ecs_task:
      name: ecs-task-role
      assume_role_policy: ${data.aws_iam_policy_document.ecs_assume_role.json}
      tags:
        Name: ecs-task-role

  aws_iam_role_policy_attachment:
    ecs_execution:
      role: ${aws_iam_role.ecs_execution.name}
      policy_arn: arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy
```

## Step 6: Create ECS Cluster and Service

Create `ecs.yaml`:

```yaml
resource:
  aws_ecs_cluster:
    main:
      name: web-app-cluster
      setting:
        - name: containerInsights
          value: enabled
      tags:
        Name: web-app-cluster

  aws_cloudwatch_log_group:
    ecs:
      name: /ecs/web-app
      retention_in_days: 7
      tags:
        Name: ecs-logs

  aws_ecs_task_definition:
    web:
      family: web-app
      network_mode: awsvpc
      requires_compatibilities:
        - FARGATE
      cpu: 256
      memory: 512
      execution_role_arn: ${aws_iam_role.ecs_execution.arn}
      task_role_arn: ${aws_iam_role.ecs_task.arn}
      container_definitions: |
        [
          {
            "name": "web",
            "image": "nginx:alpine",
            "essential": true,
            "portMappings": [
              {
                "containerPort": 80,
                "hostPort": 80,
                "protocol": "tcp"
              }
            ],
            "logConfiguration": {
              "logDriver": "awslogs",
              "options": {
                "awslogs-group": "/ecs/web-app",
                "awslogs-region": "us-west-2",
                "awslogs-stream-prefix": "web"
              }
            }
          }
        ]
      tags:
        Name: web-app-task

  aws_ecs_service:
    web:
      name: web-app-service
      cluster: ${aws_ecs_cluster.main.id}
      task_definition: ${aws_ecs_task_definition.web.arn}
      desired_count: 2
      launch_type: FARGATE

      network_configuration:
        subnets:
          - ${aws_subnet.public_a.id}
          - ${aws_subnet.public_b.id}
        security_groups:
          - ${aws_security_group.ecs.id}
        assign_public_ip: true

      load_balancer:
        - target_group_arn: ${aws_lb_target_group.ecs.arn}
          container_name: web
          container_port: 80

      depends_on:
        - aws_lb_listener.http

      tags:
        Name: web-app-service
```

## Step 7: Create Load Balancer

Create `loadbalancer.yaml`:

```yaml
resource:
  aws_lb:
    main:
      name: ecs-alb
      internal: false
      load_balancer_type: application
      security_groups:
        - ${aws_security_group.alb.id}
      subnets:
        - ${aws_subnet.public_a.id}
        - ${aws_subnet.public_b.id}
      tags:
        Name: ecs-alb

  aws_lb_target_group:
    ecs:
      name: ecs-tg
      port: 80
      protocol: HTTP
      vpc_id: ${aws_vpc.main.id}
      target_type: ip
      health_check:
        enabled: true
        path: /
        port: traffic-port
        protocol: HTTP
        healthy_threshold: 2
        unhealthy_threshold: 3
        timeout: 5
        interval: 30
        matcher: "200"
      tags:
        Name: ecs-tg

  aws_lb_listener:
    http:
      load_balancer_arn: ${aws_lb.main.arn}
      port: 80
      protocol: HTTP
      default_action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.ecs.arn}
```

## Step 8: Add Outputs

Create `outputs.yaml`:

```yaml
output:
  alb_dns_name:
    value: ${aws_lb.main.dns_name}
    description: ALB DNS name

  ecs_cluster_name:
    value: ${aws_ecs_cluster.main.name}
    description: ECS cluster name

  ecs_service_name:
    value: ${aws_ecs_service.web.name}
    description: ECS service name
```

## Step 9: Deploy

```bash
# Initialize
ytofu init

# Preview
ytofu plan

# Apply
ytofu apply
```

## Step 10: Test

1. Get the ALB DNS name from outputs
2. Open in browser: `http://<alb-dns-name>`
3. You should see the nginx welcome page

## Step 11: Scale the Service

To scale, update `desired_count` in `ecs.yaml`:

```yaml
  aws_ecs_service:
    web:
      desired_count: 4  # Scale to 4 tasks
```

Then apply:
```bash
ytofu apply
```

## Cleanup

```bash
ytofu destroy
```

## What You Learned

- ECS cluster creation
- Fargate task definitions
- Container networking with awsvpc
- IAM roles for ECS tasks
- CloudWatch log configuration
- Service discovery with ALB
- Target group with IP target type

## Next Steps

- [ECS Reference](../aws/compute/ecs.md) - Full ECS documentation
- [Blue/Green Deployment](../guides/blue-green-deployment.md) - Zero-downtime updates
- [EKS Tutorial](../aws/compute/eks.md) - Kubernetes on AWS
