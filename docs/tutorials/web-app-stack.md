# Web Application Stack

Build a complete web application infrastructure with EC2, VPC, Security Groups, and Load Balancer.

**Level:** Intermediate
**Time:** 30-45 minutes

## What You'll Build

```
┌─────────────────────────────────────────────────────────────┐
│                      VPC (10.0.0.0/16)                      │
│  ┌────────────────────┐    ┌────────────────────┐           │
│  │  Public Subnet A   │    │  Public Subnet B   │           │
│  │   (10.0.1.0/24)    │    │   (10.0.2.0/24)    │           │
│  │                    │    │                    │           │
│  │    ┌────────┐      │    │      ┌────────┐    │           │
│  │    │  EC2   │      │    │      │  EC2   │    │           │
│  │    └────┬───┘      │    │      └────┬───┘    │           │
│  └─────────┼──────────┘    └───────────┼────────┘           │
│            │                           │                    │
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

- Completed [Your First VPC](first-vpc.md) tutorial
- AWS credentials with EC2 and ELB permissions

## Step 1: Create Project Directory

```bash
mkdir web-app-stack
cd web-app-stack
```

## Step 2: Provider Configuration

Create `provider.yaml`:

```yaml
provider:
  aws:
    region: us-west-2
```

## Step 3: Create VPC with Multi-AZ Subnets

Create `vpc.yaml`:

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true
      tags:
        Name: web-app-vpc

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
  # ALB Security Group
  aws_security_group:
    alb:
      name: alb-sg
      description: Security group for ALB
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - from_port: 80
          to_port: 80
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0
          description: HTTP from internet

        - from_port: 443
          to_port: 443
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0
          description: HTTPS from internet

      egress:
        - from_port: 0
          to_port: 0
          protocol: "-1"
          cidr_blocks:
            - 0.0.0.0/0

      tags:
        Name: alb-sg

  # Web Server Security Group
  aws_security_group:
    web:
      name: web-sg
      description: Security group for web servers
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - from_port: 80
          to_port: 80
          protocol: tcp
          security_groups:
            - ${aws_security_group.alb.id}
          description: HTTP from ALB

        - from_port: 22
          to_port: 22
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0
          description: SSH access

      egress:
        - from_port: 0
          to_port: 0
          protocol: "-1"
          cidr_blocks:
            - 0.0.0.0/0

      tags:
        Name: web-sg
```

## Step 5: Create EC2 Instances

Create `compute.yaml`:

```yaml
data:
  aws_ami:
    amazon_linux:
      most_recent: true
      owners:
        - amazon
      filter:
        - name: name
          values:
            - amzn2-ami-hvm-*-x86_64-gp2

resource:
  aws_instance:
    web_a:
      ami: ${data.aws_ami.amazon_linux.id}
      instance_type: t3.micro
      subnet_id: ${aws_subnet.public_a.id}
      vpc_security_group_ids:
        - ${aws_security_group.web.id}
      user_data: |
        #!/bin/bash
        yum update -y
        yum install -y httpd
        echo "<h1>Hello from $(hostname -f)</h1>" > /var/www/html/index.html
        systemctl start httpd
        systemctl enable httpd
      tags:
        Name: web-server-a

    web_b:
      ami: ${data.aws_ami.amazon_linux.id}
      instance_type: t3.micro
      subnet_id: ${aws_subnet.public_b.id}
      vpc_security_group_ids:
        - ${aws_security_group.web.id}
      user_data: |
        #!/bin/bash
        yum update -y
        yum install -y httpd
        echo "<h1>Hello from $(hostname -f)</h1>" > /var/www/html/index.html
        systemctl start httpd
        systemctl enable httpd
      tags:
        Name: web-server-b
```

## Step 6: Create Application Load Balancer

Create `loadbalancer.yaml`:

```yaml
resource:
  aws_lb:
    main:
      name: web-app-alb
      internal: false
      load_balancer_type: application
      security_groups:
        - ${aws_security_group.alb.id}
      subnets:
        - ${aws_subnet.public_a.id}
        - ${aws_subnet.public_b.id}
      tags:
        Name: web-app-alb

  aws_lb_target_group:
    web:
      name: web-tg
      port: 80
      protocol: HTTP
      vpc_id: ${aws_vpc.main.id}
      target_type: instance
      health_check:
        enabled: true
        path: /
        port: traffic-port
        protocol: HTTP
        healthy_threshold: 2
        unhealthy_threshold: 3
        timeout: 5
        interval: 30
      tags:
        Name: web-tg

  aws_lb_listener:
    http:
      load_balancer_arn: ${aws_lb.main.arn}
      port: 80
      protocol: HTTP
      default_action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.web.arn}

  aws_lb_target_group_attachment:
    web_a:
      target_group_arn: ${aws_lb_target_group.web.arn}
      target_id: ${aws_instance.web_a.id}
      port: 80

    web_b:
      target_group_arn: ${aws_lb_target_group.web.arn}
      target_id: ${aws_instance.web_b.id}
      port: 80
```

## Step 7: Add Outputs

Create `outputs.yaml`:

```yaml
output:
  alb_dns_name:
    value: ${aws_lb.main.dns_name}
    description: ALB DNS name

  web_server_a_ip:
    value: ${aws_instance.web_a.public_ip}
    description: Web server A public IP

  web_server_b_ip:
    value: ${aws_instance.web_b.public_ip}
    description: Web server B public IP
```

## Step 8: Deploy

```bash
# Initialize
ytofu init

# Preview
ytofu plan

# Apply
ytofu apply
```

## Step 9: Test

1. Get the ALB DNS name from outputs
2. Open in browser: `http://<alb-dns-name>`
3. Refresh to see traffic distributed between servers

## Cleanup

```bash
ytofu destroy
```

## What You Learned

- Multi-AZ subnet deployment
- Security group chaining (ALB → EC2)
- User data for instance initialization
- Application Load Balancer setup
- Target group configuration
- Health checks

## Next Steps

- [Container Deployment](container-deployment.md) - Deploy with ECS Fargate
- [Multi-AZ Deployment Guide](../guides/multi-az-deployment.md) - Production patterns
- [Load Balancer Reference](../aws/networking/load-balancer.md) - Full documentation
