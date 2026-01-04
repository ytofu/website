# Your First VPC

Create a VPC with public subnet and internet access.

**Level:** Beginner
**Time:** 15-20 minutes

## What You'll Build

```
┌─────────────────────────────────────┐
│              VPC (10.0.0.0/16)      │
│  ┌─────────────────────────────┐    │
│  │     Public Subnet           │    │
│  │     (10.0.1.0/24)           │    │
│  └──────────────┬──────────────┘    │
│                 │                   │
│          ┌──────┴──────┐            │
│          │     IGW     │            │
│          └──────┬──────┘            │
└─────────────────┼───────────────────┘
                  │
              Internet
```

## Prerequisites

- ytofu installed ([Getting Started](../getting-started.md))
- AWS credentials configured
- A text editor

## Step 1: Create Project Directory

```bash
mkdir my-first-vpc
cd my-first-vpc
```

## Step 2: Configure AWS Provider

Create `provider.yaml`:

```yaml
provider:
  aws:
    region: us-west-2
```

## Step 3: Create the VPC

Create `main.yaml`:

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true
      tags:
        Name: my-first-vpc
```

**What this does:**
- Creates a VPC with IP range 10.0.0.0/16 (65,536 addresses)
- Enables DNS hostnames for resources
- Tags the VPC for easy identification

## Step 4: Add a Public Subnet

Add to `main.yaml`:

```yaml
  aws_subnet:
    public:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet
```

**What this does:**
- Creates a subnet within the VPC
- Uses IP range 10.0.1.0/24 (256 addresses)
- Automatically assigns public IPs to instances

## Step 5: Add Internet Gateway

Add to `main.yaml`:

```yaml
  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-igw
```

**What this does:**
- Attaches an Internet Gateway to the VPC
- Enables internet connectivity for resources

## Step 6: Create Route Table

Add to `main.yaml`:

```yaml
  aws_route_table:
    public:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}
      tags:
        Name: public-rt

  aws_route_table_association:
    public:
      subnet_id: ${aws_subnet.public.id}
      route_table_id: ${aws_route_table.public.id}
```

**What this does:**
- Creates a route table with internet route (0.0.0.0/0 via IGW)
- Associates the route table with the public subnet

## Complete Configuration

Your `main.yaml` should look like this:

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true
      tags:
        Name: my-first-vpc

  aws_subnet:
    public:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet

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
    public:
      subnet_id: ${aws_subnet.public.id}
      route_table_id: ${aws_route_table.public.id}
```

## Step 7: Initialize and Apply

```bash
# Initialize ytofu
ytofu init

# Preview changes
ytofu plan

# Apply changes
ytofu apply
```

Type `yes` when prompted to confirm.

## Step 8: Verify

Check your resources in the AWS Console:
1. Go to VPC Dashboard
2. Find "my-first-vpc"
3. Verify subnet and internet gateway are attached

## Cleanup

When you're done, destroy the resources:

```bash
ytofu destroy
```

Type `yes` to confirm.

## What You Learned

- Creating a VPC with CIDR block
- Adding subnets to a VPC
- Attaching an Internet Gateway
- Configuring route tables for internet access
- Using resource references (`${aws_vpc.main.id}`)

## Next Steps

- [Web Application Stack](web-app-stack.md) - Add EC2, security groups, and load balancer
- [VPC Reference](../aws/networking/vpc.md) - Full VPC documentation
- [Security Groups](../aws/networking/security-groups.md) - Control network traffic
