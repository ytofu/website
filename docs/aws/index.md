# AWS Provider

Configure and use the AWS provider with ytofu YAML syntax.

## Configuration as Data

ytofu follows the **Configuration as Data** paradigm for Terraform. Unlike HCL, ytofu YAML configurations are pure data without programming constructs:

- **No for loops** - Define each resource explicitly
- **No variables** - Use concrete values
- **No conditionals** - No ternary expressions or if statements
- **No functions** - No `cidrsubnet()`, `lookup()`, etc.
- **Simple references only** - `${aws_vpc.main.id}` is acceptable

This approach makes configurations:
- Easier to read and understand
- Simpler to generate from external tools
- Compatible with GitOps workflows
- Auditable as plain data

## Provider Configuration

```yaml
terraform:
  required_providers:
    aws:
      source: hashicorp/aws
      version: "~> 5.0"

provider:
  aws:
    region: us-west-2
```

## Authentication

ytofu supports all standard AWS authentication methods:

### Environment Variables

```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_REGION="us-west-2"
```

### Shared Credentials File

```yaml
provider:
  aws:
    region: us-west-2
    profile: my-profile
```

### IAM Role (EC2/ECS)

When running on AWS infrastructure, ytofu automatically uses the attached IAM role.

```yaml
provider:
  aws:
    region: us-west-2
```

## Multiple Regions

Use provider aliases for multi-region deployments:

```yaml
provider:
  aws:
    region: us-west-2

  aws.east:
    region: us-east-1
    alias: east

resource:
  aws_instance:
    west_server:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.micro

    east_server:
      provider: aws.east
      ami: ami-0123456789abcdef0
      instance_type: t3.micro
```

## Common Arguments

| Argument | Type | Description |
|----------|------|-------------|
| region | string | AWS region |
| profile | string | AWS credentials profile name |
| access_key | string | AWS access key (not recommended) |
| secret_key | string | AWS secret key (not recommended) |
| assume_role | object | IAM role to assume |
| default_tags | object | Tags applied to all resources |

## Default Tags

Apply tags to all resources automatically:

```yaml
provider:
  aws:
    region: us-west-2
    default_tags:
      tags:
        Environment: production
        Project: ytofu-demo
        ManagedBy: ytofu
```

## Resources

- [Compute](compute/index.md) - EC2, Lambda, ECS, EKS
- [Networking](networking/index.md) - VPC, Subnets, Security Groups, Load Balancers

## Resource Index

Quick reference to all documented AWS resources.

### Compute

| Resource | Type | Description |
|----------|------|-------------|
| [EC2 Instance](compute/ec2-instance.md) | `aws_instance` | Virtual servers |
| [Lambda](compute/lambda.md) | `aws_lambda_function` | Serverless functions |
| [ECS](compute/ecs.md) | `aws_ecs_cluster`, `aws_ecs_service` | Container orchestration |
| [EKS](compute/eks.md) | `aws_eks_cluster` | Managed Kubernetes |
| [Launch Template](compute/launch-template.md) | `aws_launch_template` | EC2 launch configuration |
| [Auto Scaling](compute/autoscaling.md) | `aws_autoscaling_group` | Automatic scaling |

### Networking

| Resource | Type | Description |
|----------|------|-------------|
| [VPC](networking/vpc.md) | `aws_vpc`, `aws_subnet` | Virtual network |
| [Security Groups](networking/security-groups.md) | `aws_security_group` | Firewall rules |
| [Internet Gateway](networking/internet-gateway.md) | `aws_internet_gateway` | Public internet access |
| [NAT Gateway](networking/nat-gateway.md) | `aws_nat_gateway` | Private subnet internet |
| [Load Balancer](networking/load-balancer.md) | `aws_lb`, `aws_lb_listener` | Traffic distribution |
| [Route Tables](networking/route-tables.md) | `aws_route_table` | Network routing |
| [Route53](networking/route53.md) | `aws_route53_zone`, `aws_route53_record` | DNS management |
