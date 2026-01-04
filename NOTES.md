# ytofu Website Development Notes

## Project Overview

- **Repository:** https://github.com/ytofu/website
- **Live Site:** https://ytofu.github.io/website/
- **Framework:** MkDocs with Material theme
- **Deployment:** GitHub Actions → GitHub Pages

## What is ytofu?

OpenTofu fork with first-class YAML support following the **Configuration as Data** paradigm:
- No for loops, variables, conditionals, or functions
- Pure YAML data, not code
- Simple resource references only (`${aws_resource.name.id}`)

## Documentation Structure (Diátaxis Framework)

```
docs/
├── index.md                 # Home
├── getting-started.md       # Quick start
├── concepts/                # EXPLANATION - Why/What
│   ├── configuration-as-data.md
│   ├── yaml-vs-hcl.md
│   └── resource-lifecycle.md
├── tutorials/               # LEARNING - Step-by-step
│   ├── first-vpc.md         # Beginner
│   ├── web-app-stack.md     # Intermediate
│   └── container-deployment.md  # Advanced
├── guides/                  # HOW-TO - Task-oriented
│   ├── multi-az-deployment.md
│   ├── private-public-subnets.md
│   └── blue-green-deployment.md
├── aws/                     # REFERENCE - Facts
│   ├── compute/             # EC2, Lambda, ECS, EKS
│   └── networking/          # VPC, SG, IGW, NAT, LB, Route53
└── troubleshooting/         # Problem solving
    └── common-errors.md
```

## Key Commits

1. **44561e2** - Initial ytofu documentation website
2. **4ba655e** - Add comprehensive AWS provider documentation (15 resource docs)
3. **2c71b11** - Reorganize documentation using Diátaxis framework (14 new files)

## Configuration as Data Rules

When writing examples, AVOID:
- `for_each`, `count`, `for` expressions
- `${var.xxx}` variable references
- Functions like `cidrsubnet()`, `lookup()`
- Conditionals and dynamic blocks

USE instead:
- Explicit values
- Explicit resource definitions (one per resource)
- Simple resource references for relationships

## AWS Resources Documented

### Compute
- EC2 Instance (`aws_instance`)
- Lambda (`aws_lambda_function`)
- ECS (`aws_ecs_cluster`, `aws_ecs_service`)
- EKS (`aws_eks_cluster`)
- Launch Template (`aws_launch_template`)
- Auto Scaling (`aws_autoscaling_group`)

### Networking
- VPC (`aws_vpc`, `aws_subnet`)
- Security Groups (`aws_security_group`)
- Internet Gateway (`aws_internet_gateway`)
- NAT Gateway (`aws_nat_gateway`)
- Load Balancer (`aws_lb`, `aws_lb_listener`)
- Route Tables (`aws_route_table`)
- Route53 (`aws_route53_zone`, `aws_route53_record`)

## Future Work

Potential additions:
- Storage (S3, EBS, EFS)
- Database (RDS, DynamoDB)
- IAM (Roles, Policies)
- Other providers (GCP, Azure)
- More tutorials and guides
