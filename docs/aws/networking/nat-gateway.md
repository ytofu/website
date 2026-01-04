# NAT Gateway

A NAT Gateway allows private subnets to access the internet for outbound traffic while preventing inbound connections.

## Basic Example

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
      subnet_id: ${aws_subnet.public.id}
      tags:
        Name: main-nat

      depends_on:
        - aws_internet_gateway.main
```

## Complete Private Subnet Setup

```yaml
resource:
  # VPC
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      tags:
        Name: main-vpc

  # Internet Gateway
  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-igw

  # Public Subnet (for NAT Gateway)
  aws_subnet:
    public:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet

  # Private Subnet
  aws_subnet:
    private:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.10.0/24
      availability_zone: us-west-2a
      tags:
        Name: private-subnet

  # Elastic IP for NAT
  aws_eip:
    nat:
      domain: vpc
      tags:
        Name: nat-eip

  # NAT Gateway
  aws_nat_gateway:
    main:
      allocation_id: ${aws_eip.nat.id}
      subnet_id: ${aws_subnet.public.id}
      tags:
        Name: main-nat
      depends_on:
        - aws_internet_gateway.main

  # Public Route Table
  aws_route_table:
    public:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}
      tags:
        Name: public-rt

  # Private Route Table
  aws_route_table:
    private:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          nat_gateway_id: ${aws_nat_gateway.main.id}
      tags:
        Name: private-rt

  # Route Table Associations
  aws_route_table_association:
    public:
      subnet_id: ${aws_subnet.public.id}
      route_table_id: ${aws_route_table.public.id}

    private:
      subnet_id: ${aws_subnet.private.id}
      route_table_id: ${aws_route_table.private.id}
```

## Arguments Reference

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| allocation_id | string | Yes* | Elastic IP allocation ID |
| subnet_id | string | Yes | Public subnet ID |
| connectivity_type | string | No | "public" (default) or "private" |
| tags | map | No | Resource tags |

*Required for public NAT Gateway

## Common Patterns

### Multi-AZ NAT Gateways

For high availability, deploy a NAT Gateway in each AZ:

```yaml
resource:
  # AZ A
  aws_eip:
    nat_a:
      domain: vpc
      tags:
        Name: nat-eip-a

  aws_nat_gateway:
    a:
      allocation_id: ${aws_eip.nat_a.id}
      subnet_id: ${aws_subnet.public_a.id}
      tags:
        Name: nat-a

  aws_route_table:
    private_a:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          nat_gateway_id: ${aws_nat_gateway.a.id}
      tags:
        Name: private-rt-a

  aws_route_table_association:
    private_a:
      subnet_id: ${aws_subnet.private_a.id}
      route_table_id: ${aws_route_table.private_a.id}

  # AZ B
  aws_eip:
    nat_b:
      domain: vpc
      tags:
        Name: nat-eip-b

  aws_nat_gateway:
    b:
      allocation_id: ${aws_eip.nat_b.id}
      subnet_id: ${aws_subnet.public_b.id}
      tags:
        Name: nat-b

  aws_route_table:
    private_b:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          nat_gateway_id: ${aws_nat_gateway.b.id}
      tags:
        Name: private-rt-b

  aws_route_table_association:
    private_b:
      subnet_id: ${aws_subnet.private_b.id}
      route_table_id: ${aws_route_table.private_b.id}
```

### Private NAT Gateway (VPC-to-VPC)

```yaml
resource:
  aws_nat_gateway:
    private:
      connectivity_type: private
      subnet_id: ${aws_subnet.private.id}
      tags:
        Name: private-nat
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | NAT Gateway ID |
| public_ip | Public IP address |
| private_ip | Private IP address |
| network_interface_id | Network interface ID |

## Cost Considerations

| Item | Pricing |
|------|---------|
| NAT Gateway | ~$0.045/hour + $0.045/GB processed |
| Elastic IP (attached) | Free |
| Elastic IP (unattached) | ~$0.005/hour |

## Best Practices

- **Use NAT Gateway per AZ** for high availability
- **Delete unused EIPs** to avoid charges
- **Consider VPC Endpoints** for AWS services to reduce NAT costs
- **Monitor data processing** through NAT Gateway
- **Use private NAT** for VPC-to-VPC communication
- **Ensure IGW exists** before creating NAT Gateway

## Troubleshooting

| Issue | Solution |
|-------|----------|
| No internet from private subnet | Check NAT Gateway route in private route table |
| NAT Gateway stuck creating | Ensure IGW is attached to VPC |
| EIP in use error | Release EIP from previous NAT Gateway |
| High data transfer costs | Use VPC Endpoints for AWS services |

## Related Resources

- [Internet Gateway](internet-gateway.md)
- [VPC](vpc.md)
- [Route Tables](route-tables.md)
- [Security Groups](security-groups.md)
