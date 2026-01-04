# Multi-AZ Deployment

Deploy resources across multiple Availability Zones for high availability.

## Problem

You need to ensure your application remains available even if an entire data center fails.

## Solution

Deploy resources across multiple Availability Zones (AZs) with load balancing.

## Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           VPC (10.0.0.0/16)                             │
│                                                                         │
│  ┌─────────────────────┐  ┌─────────────────────┐  ┌─────────────────┐  │
│  │   AZ: us-west-2a    │  │   AZ: us-west-2b    │  │   AZ: us-west-2c│  │
│  │                     │  │                     │  │                 │  │
│  │ ┌─────────────────┐ │  │ ┌─────────────────┐ │  │ ┌─────────────┐ │  │
│  │ │ Public Subnet   │ │  │ │ Public Subnet   │ │  │ │ Public Sub  │ │  │
│  │ │ 10.0.1.0/24     │ │  │ │ 10.0.2.0/24     │ │  │ │ 10.0.3.0/24 │ │  │
│  │ │   [EC2/ECS]     │ │  │ │   [EC2/ECS]     │ │  │ │  [EC2/ECS]  │ │  │
│  │ └────────┬────────┘ │  │ └────────┬────────┘ │  │ └──────┬──────┘ │  │
│  │          │          │  │          │          │  │        │        │  │
│  │ ┌────────┴────────┐ │  │ ┌────────┴────────┐ │  │ ┌──────┴──────┐ │  │
│  │ │ Private Subnet  │ │  │ │ Private Subnet  │ │  │ │ Private Sub │ │  │
│  │ │ 10.0.11.0/24    │ │  │ │ 10.0.12.0/24    │ │  │ │ 10.0.13.0/24│ │  │
│  │ │     [RDS]       │ │  │ │     [RDS]       │ │  │ │    [RDS]    │ │  │
│  │ └─────────────────┘ │  │ └─────────────────┘ │  │ └─────────────┘ │  │
│  └─────────────────────┘  └─────────────────────┘  └─────────────────┘  │
│                                    │                                    │
│                             ┌──────┴──────┐                             │
│                             │     ALB     │                             │
│                             └─────────────┘                             │
└─────────────────────────────────────────────────────────────────────────┘
```

## Configuration

### VPC with Multi-AZ Subnets

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true
      tags:
        Name: multi-az-vpc

  # Public Subnets - One per AZ
  aws_subnet:
    public_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet-a
        Tier: public

    public_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.2.0/24
      availability_zone: us-west-2b
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet-b
        Tier: public

    public_c:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.3.0/24
      availability_zone: us-west-2c
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet-c
        Tier: public

  # Private Subnets - One per AZ
  aws_subnet:
    private_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.11.0/24
      availability_zone: us-west-2a
      tags:
        Name: private-subnet-a
        Tier: private

    private_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.12.0/24
      availability_zone: us-west-2b
      tags:
        Name: private-subnet-b
        Tier: private

    private_c:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.13.0/24
      availability_zone: us-west-2c
      tags:
        Name: private-subnet-c
        Tier: private
```

### Internet Gateway and Public Routes

```yaml
resource:
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

    public_c:
      subnet_id: ${aws_subnet.public_c.id}
      route_table_id: ${aws_route_table.public.id}
```

### NAT Gateways (One per AZ for HA)

```yaml
resource:
  aws_eip:
    nat_a:
      domain: vpc
      tags:
        Name: nat-eip-a

    nat_b:
      domain: vpc
      tags:
        Name: nat-eip-b

    nat_c:
      domain: vpc
      tags:
        Name: nat-eip-c

  aws_nat_gateway:
    a:
      allocation_id: ${aws_eip.nat_a.id}
      subnet_id: ${aws_subnet.public_a.id}
      tags:
        Name: nat-a
      depends_on:
        - aws_internet_gateway.main

    b:
      allocation_id: ${aws_eip.nat_b.id}
      subnet_id: ${aws_subnet.public_b.id}
      tags:
        Name: nat-b
      depends_on:
        - aws_internet_gateway.main

    c:
      allocation_id: ${aws_eip.nat_c.id}
      subnet_id: ${aws_subnet.public_c.id}
      tags:
        Name: nat-c
      depends_on:
        - aws_internet_gateway.main

  # Private route tables - one per AZ
  aws_route_table:
    private_a:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          nat_gateway_id: ${aws_nat_gateway.a.id}
      tags:
        Name: private-rt-a

    private_b:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          nat_gateway_id: ${aws_nat_gateway.b.id}
      tags:
        Name: private-rt-b

    private_c:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          nat_gateway_id: ${aws_nat_gateway.c.id}
      tags:
        Name: private-rt-c

  aws_route_table_association:
    private_a:
      subnet_id: ${aws_subnet.private_a.id}
      route_table_id: ${aws_route_table.private_a.id}

    private_b:
      subnet_id: ${aws_subnet.private_b.id}
      route_table_id: ${aws_route_table.private_b.id}

    private_c:
      subnet_id: ${aws_subnet.private_c.id}
      route_table_id: ${aws_route_table.private_c.id}
```

### Application Load Balancer

```yaml
resource:
  aws_lb:
    main:
      name: multi-az-alb
      internal: false
      load_balancer_type: application
      security_groups:
        - ${aws_security_group.alb.id}
      subnets:
        - ${aws_subnet.public_a.id}
        - ${aws_subnet.public_b.id}
        - ${aws_subnet.public_c.id}
      tags:
        Name: multi-az-alb
```

## Key Considerations

### Number of AZs

| AZs | Availability | Cost | Use Case |
|-----|--------------|------|----------|
| 2 | 99.99% | Lower | Development, staging |
| 3 | 99.999% | Higher | Production workloads |

### NAT Gateway Strategy

| Strategy | Availability | Cost |
|----------|--------------|------|
| 1 NAT Gateway | Low | ~$32/month |
| NAT per AZ | High | ~$96/month (3 AZs) |

### Database Multi-AZ

For RDS, enable Multi-AZ deployment:

```yaml
resource:
  aws_db_instance:
    main:
      multi_az: true
      # ... other settings
```

## Best Practices

- **Use at least 2 AZs** for production workloads
- **Use 3 AZs** for critical applications
- **Place NAT Gateway per AZ** for true high availability
- **Distribute compute evenly** across AZs
- **Use ALB** for automatic health checks and failover

## Related Resources

- [VPC Reference](../aws/networking/vpc.md)
- [NAT Gateway](../aws/networking/nat-gateway.md)
- [Load Balancer](../aws/networking/load-balancer.md)
- [Private/Public Subnets](private-public-subnets.md)
