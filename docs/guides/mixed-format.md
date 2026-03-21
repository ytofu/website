# Mixed Format Workflow

This guide shows how to combine HCL and YAML files in the same ytofu project, leveraging the strengths of each format.

## Overview

The mixed format workflow uses:
- **HCL files** (`.tf`) for variables, locals, and complex logic
- **YAML files** (`.yaml`) for resource definitions

This approach gives you the best of both worlds: type-safe variables with defaults, computed locals, and clean YAML resource definitions that are easy to generate and review.

## Project Structure

```
project/
├── variables.tf       # Variable definitions (HCL)
├── locals.tf          # Computed values (HCL)
├── providers.tf       # Provider configuration (HCL)
├── main.yaml          # Resource definitions (YAML)
├── networking.yaml    # Network resources (YAML)
└── terraform.tfvars   # Variable values
```

## Step 1: Define Variables in HCL

Create `variables.tf` with your input variables:

```hcl
# variables.tf

variable "environment" {
  description = "Deployment environment"
  type        = string
  default     = "dev"

  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "Environment must be dev, staging, or prod."
  }
}

variable "project_name" {
  description = "Project name for resource naming"
  type        = string
}

variable "vpc_cidr" {
  description = "CIDR block for the VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "availability_zones" {
  description = "List of availability zones"
  type        = list(string)
  default     = ["us-west-2a", "us-west-2b"]
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t3.micro"
}

variable "enable_monitoring" {
  description = "Enable CloudWatch monitoring"
  type        = bool
  default     = false
}
```

## Step 2: Define Locals in HCL

Create `locals.tf` for computed values:

```hcl
# locals.tf

locals {
  # Naming convention
  name_prefix = "${var.project_name}-${var.environment}"

  # Common tags applied to all resources
  common_tags = {
    Project     = var.project_name
    Environment = var.environment
    ManagedBy   = "ytofu"
  }

  # Environment-specific settings
  is_production = var.environment == "prod"

  # Computed CIDR blocks for subnets
  public_subnet_cidrs = [
    cidrsubnet(var.vpc_cidr, 8, 1),
    cidrsubnet(var.vpc_cidr, 8, 2)
  ]

  private_subnet_cidrs = [
    cidrsubnet(var.vpc_cidr, 8, 10),
    cidrsubnet(var.vpc_cidr, 8, 11)
  ]
}
```

## Step 3: Configure Providers in HCL

Create `providers.tf`:

```hcl
# providers.tf

terraform {
  required_version = ">= 1.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-west-2"

  default_tags {
    tags = local.common_tags
  }
}
```

## Step 4: Define Resources in YAML

Create `networking.yaml` for network resources:

```yaml
# networking.yaml

resource:
  aws_vpc:
    main:
      cidr_block: ${var.vpc_cidr}
      enable_dns_hostnames: true
      enable_dns_support: true
      tags:
        Name: ${local.name_prefix}-vpc

  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: ${local.name_prefix}-igw

  aws_subnet:
    public_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: ${local.public_subnet_cidrs[0]}
      availability_zone: ${var.availability_zones[0]}
      map_public_ip_on_launch: true
      tags:
        Name: ${local.name_prefix}-public-a
        Type: public

    public_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: ${local.public_subnet_cidrs[1]}
      availability_zone: ${var.availability_zones[1]}
      map_public_ip_on_launch: true
      tags:
        Name: ${local.name_prefix}-public-b
        Type: public

  aws_route_table:
    public:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}
      tags:
        Name: ${local.name_prefix}-public-rt

  aws_route_table_association:
    public_a:
      subnet_id: ${aws_subnet.public_a.id}
      route_table_id: ${aws_route_table.public.id}

    public_b:
      subnet_id: ${aws_subnet.public_b.id}
      route_table_id: ${aws_route_table.public.id}
```

Create `main.yaml` for compute resources:

```yaml
# main.yaml

resource:
  aws_security_group:
    web:
      name: ${local.name_prefix}-web-sg
      description: Security group for web servers
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - description: HTTP
          from_port: 80
          to_port: 80
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0

        - description: HTTPS
          from_port: 443
          to_port: 443
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
        Name: ${local.name_prefix}-web-sg

  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: ${var.instance_type}
      subnet_id: ${aws_subnet.public_a.id}
      vpc_security_group_ids:
        - ${aws_security_group.web.id}
      monitoring: ${var.enable_monitoring}
      tags:
        Name: ${local.name_prefix}-web

output:
  vpc_id:
    value: ${aws_vpc.main.id}
    description: ID of the VPC

  public_subnet_ids:
    value:
      - ${aws_subnet.public_a.id}
      - ${aws_subnet.public_b.id}
    description: IDs of public subnets

  web_instance_id:
    value: ${aws_instance.web.id}
    description: ID of the web instance
```

## Step 5: Set Variable Values

Create `terraform.tfvars`:

```hcl
project_name      = "myapp"
environment       = "dev"
vpc_cidr          = "10.0.0.0/16"
instance_type     = "t3.micro"
enable_monitoring = false
```

Or for production:

```hcl
# terraform.prod.tfvars
project_name      = "myapp"
environment       = "prod"
vpc_cidr          = "10.1.0.0/16"
instance_type     = "t3.large"
enable_monitoring = true
```

## Step 6: Deploy

```bash
# Initialize
ytofu init

# Plan (development)
ytofu plan

# Plan (production)
ytofu plan -var-file="terraform.prod.tfvars"

# Apply
ytofu apply
```

## Benefits of This Approach

### Type Safety

Variables in HCL provide type checking and validation:

```hcl
variable "port" {
  type = number  # Prevents string values

  validation {
    condition     = var.port > 0 && var.port < 65536
    error_message = "Port must be between 1 and 65535."
  }
}
```

### Computed Values

Locals in HCL can use functions not available in YAML:

```hcl
locals {
  # Use functions
  subnet_cidrs = [for i in range(4) : cidrsubnet(var.vpc_cidr, 8, i)]

  # Conditional logic
  instance_type = var.environment == "prod" ? "t3.large" : "t3.micro"

  # Merging maps
  all_tags = merge(local.common_tags, var.extra_tags)
}
```

### Clean Resource Definitions

YAML resources are pure data, easy to read and generate:

```yaml
resource:
  aws_instance:
    web:
      ami: ${var.ami_id}
      instance_type: ${local.instance_type}
      tags: ${local.all_tags}
```

### Easy Generation

Generate YAML from external tools:

```python
import yaml

resources = {
    'resource': {
        'aws_instance': {
            'web': {
                'ami': '${var.ami_id}',
                'instance_type': '${local.instance_type}',
                'tags': '${local.all_tags}'
            }
        }
    }
}

with open('generated.yaml', 'w') as f:
    yaml.dump(resources, f)
```

## Best Practices

1. **Keep HCL files focused** - Variables, locals, providers only
2. **Keep YAML files clean** - Resources and outputs only
3. **Use locals for computation** - Compute values in HCL, reference in YAML
4. **Consistent naming** - Use `local.name_prefix` for all resource names
5. **Common tags** - Define once in locals, apply everywhere
6. **Separate by concern** - networking.yaml, compute.yaml, database.yaml

## When to Use Each Format

| Content | Use HCL | Use YAML |
|---------|---------|----------|
| Variables with types | Yes | No |
| Variables with validation | Yes | No |
| Locals with functions | Yes | No |
| Provider configuration | Yes | Possible |
| Simple resources | Possible | Yes |
| Generated resources | No | Yes |
| GitOps manifests | No | Yes |

## Related

- [Configuration as Data](../concepts/configuration-as-data.md)
- [YAML vs HCL](../concepts/yaml-vs-hcl.md)
- [Getting Started](../getting-started.md)
