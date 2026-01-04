# Private and Public Subnets

Implement network isolation with separate public and private subnets.

## Problem

You need to protect backend resources (databases, internal services) from direct internet access while allowing them to make outbound connections.

## Solution

Create a VPC with public subnets (internet-facing) and private subnets (internal only), connected via NAT Gateway.

## Architecture

```
                         Internet
                            │
                     ┌──────┴──────┐
                     │     IGW     │
                     └──────┬──────┘
                            │
┌───────────────────────────┼───────────────────────────┐
│                    VPC    │                           │
│  ┌────────────────────────┴──────────────────────┐    │
│  │              Public Subnets                    │    │
│  │  ┌─────────────┐              ┌─────────────┐  │    │
│  │  │   Web/LB    │              │   NAT GW    │  │    │
│  │  └──────┬──────┘              └──────┬──────┘  │    │
│  └─────────┼────────────────────────────┼─────────┘    │
│            │                            │              │
│  ┌─────────┴────────────────────────────┴─────────┐    │
│  │              Private Subnets                    │    │
│  │  ┌─────────────┐              ┌─────────────┐  │    │
│  │  │   App/API   │              │  Database   │  │    │
│  │  └─────────────┘              └─────────────┘  │    │
│  └────────────────────────────────────────────────┘    │
└────────────────────────────────────────────────────────┘
```

## When to Use

| Scenario | Public Subnet | Private Subnet |
|----------|---------------|----------------|
| Load balancers | Yes | No |
| Web servers (public) | Yes | No |
| Application servers | No | Yes |
| Databases | No | Yes |
| Internal APIs | No | Yes |
| Bastion hosts | Yes | No |
| NAT Gateways | Yes | No |

## Configuration

### VPC and Subnets

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      enable_dns_support: true
      tags:
        Name: isolated-vpc

  # Public Subnets
  aws_subnet:
    public_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet-a
        Type: public

    public_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.2.0/24
      availability_zone: us-west-2b
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet-b
        Type: public

  # Private Subnets
  aws_subnet:
    private_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.10.0/24
      availability_zone: us-west-2a
      tags:
        Name: private-subnet-a
        Type: private

    private_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.11.0/24
      availability_zone: us-west-2b
      tags:
        Name: private-subnet-b
        Type: private
```

### Internet Gateway (Public Access)

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
```

### NAT Gateway (Private Outbound)

```yaml
resource:
  aws_eip:
    nat:
      domain: vpc
      tags:
        Name: nat-eip

  aws_nat_gateway:
    main:
      allocation_id: ${aws_eip.nat.id}
      subnet_id: ${aws_subnet.public_a.id}
      tags:
        Name: main-nat
      depends_on:
        - aws_internet_gateway.main

  aws_route_table:
    private:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          nat_gateway_id: ${aws_nat_gateway.main.id}
      tags:
        Name: private-rt

  aws_route_table_association:
    private_a:
      subnet_id: ${aws_subnet.private_a.id}
      route_table_id: ${aws_route_table.private.id}

    private_b:
      subnet_id: ${aws_subnet.private_b.id}
      route_table_id: ${aws_route_table.private.id}
```

### Security Groups

```yaml
resource:
  # ALB Security Group (Public)
  aws_security_group:
    alb:
      name: alb-sg
      description: ALB security group
      vpc_id: ${aws_vpc.main.id}

      ingress:
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

  # App Security Group (Private)
  aws_security_group:
    app:
      name: app-sg
      description: Application security group
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - from_port: 8080
          to_port: 8080
          protocol: tcp
          security_groups:
            - ${aws_security_group.alb.id}
          description: From ALB only

      egress:
        - from_port: 0
          to_port: 0
          protocol: "-1"
          cidr_blocks:
            - 0.0.0.0/0

      tags:
        Name: app-sg

  # Database Security Group (Private)
  aws_security_group:
    db:
      name: db-sg
      description: Database security group
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - from_port: 5432
          to_port: 5432
          protocol: tcp
          security_groups:
            - ${aws_security_group.app.id}
          description: From app only

      egress:
        - from_port: 0
          to_port: 0
          protocol: "-1"
          cidr_blocks:
            - 0.0.0.0/0

      tags:
        Name: db-sg
```

## Traffic Flow

### Inbound (Internet → Private)

```
Internet → IGW → ALB (public) → App (private) → DB (private)
```

1. Request arrives at ALB in public subnet
2. ALB forwards to app in private subnet
3. App queries database in private subnet
4. Response returns through ALB

### Outbound (Private → Internet)

```
Private Subnet → NAT Gateway (public) → IGW → Internet
```

1. Private resource initiates connection
2. Traffic routes to NAT Gateway
3. NAT Gateway sends to Internet Gateway
4. Response returns through same path

## CIDR Planning

| Subnet Type | CIDR Range | Available IPs |
|-------------|------------|---------------|
| Public A | 10.0.1.0/24 | 251 |
| Public B | 10.0.2.0/24 | 251 |
| Private A | 10.0.10.0/24 | 251 |
| Private B | 10.0.11.0/24 | 251 |

**Tip:** Leave gaps in CIDR ranges for future expansion.

## Best Practices

- **Never place databases in public subnets**
- **Use security group chaining** (ALB → App → DB)
- **Minimize public subnet resources**
- **Use VPC Endpoints** for AWS services to reduce NAT costs
- **Tag subnets** with Type: public/private for clarity

## Related Resources

- [VPC Reference](../aws/networking/vpc.md)
- [Security Groups](../aws/networking/security-groups.md)
- [NAT Gateway](../aws/networking/nat-gateway.md)
- [Multi-AZ Deployment](multi-az-deployment.md)
