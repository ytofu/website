# Route Tables

Manage VPC routing with ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route_table:
    public:
      vpc_id: ${aws_vpc.main.id}

      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}

      tags:
        Name: public-rt
```

## With Association

```yaml
resource:
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

## Arguments Reference (Route Table)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| vpc_id | string | Yes | VPC ID |
| route | list | No | List of routes |
| tags | map | No | Resource tags |

### Route Arguments

| Argument | Type | Description |
|----------|------|-------------|
| cidr_block | string | Destination CIDR |
| ipv6_cidr_block | string | Destination IPv6 CIDR |
| gateway_id | string | Internet Gateway ID |
| nat_gateway_id | string | NAT Gateway ID |
| transit_gateway_id | string | Transit Gateway ID |
| vpc_peering_connection_id | string | VPC Peering ID |
| vpc_endpoint_id | string | VPC Endpoint ID |

## Common Patterns

### Public and Private Route Tables

```yaml
resource:
  # Internet Gateway
  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-igw

  # NAT Gateway
  aws_eip:
    nat:
      domain: vpc

  aws_nat_gateway:
    main:
      allocation_id: ${aws_eip.nat.id}
      subnet_id: ${aws_subnet.public_a.id}
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

  # Associations
  aws_route_table_association:
    public_a:
      subnet_id: ${aws_subnet.public_a.id}
      route_table_id: ${aws_route_table.public.id}

    public_b:
      subnet_id: ${aws_subnet.public_b.id}
      route_table_id: ${aws_route_table.public.id}

    private_a:
      subnet_id: ${aws_subnet.private_a.id}
      route_table_id: ${aws_route_table.private.id}

    private_b:
      subnet_id: ${aws_subnet.private_b.id}
      route_table_id: ${aws_route_table.private.id}
```

### VPC Peering Route

```yaml
resource:
  aws_route_table:
    with_peering:
      vpc_id: ${aws_vpc.main.id}

      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}

        - cidr_block: 10.1.0.0/16  # Peer VPC CIDR
          vpc_peering_connection_id: ${aws_vpc_peering_connection.peer.id}

      tags:
        Name: rt-with-peering
```

### Transit Gateway Route

```yaml
resource:
  aws_route_table:
    with_tgw:
      vpc_id: ${aws_vpc.main.id}

      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}

        - cidr_block: 10.0.0.0/8  # All internal networks
          transit_gateway_id: ${aws_ec2_transit_gateway.main.id}

      tags:
        Name: rt-with-tgw
```

## Using Separate Route Resources

For dynamic routes or avoiding inline route replacement:

```yaml
resource:
  aws_route_table:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-rt

  aws_route:
    internet:
      route_table_id: ${aws_route_table.main.id}
      destination_cidr_block: 0.0.0.0/0
      gateway_id: ${aws_internet_gateway.main.id}

    peering:
      route_table_id: ${aws_route_table.main.id}
      destination_cidr_block: 10.1.0.0/16
      vpc_peering_connection_id: ${aws_vpc_peering_connection.peer.id}
```

## Arguments Reference (aws_route)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| route_table_id | string | Yes | Route table ID |
| destination_cidr_block | string | Yes* | Destination CIDR |
| destination_ipv6_cidr_block | string | Yes* | Destination IPv6 |
| gateway_id | string | No | Internet Gateway ID |
| nat_gateway_id | string | No | NAT Gateway ID |
| transit_gateway_id | string | No | Transit Gateway ID |
| vpc_peering_connection_id | string | No | VPC Peering ID |

*One of cidr_block or ipv6_cidr_block required

## Default Route Table

Modify the VPC's default route table:

```yaml
resource:
  aws_default_route_table:
    default:
      default_route_table_id: ${aws_vpc.main.default_route_table_id}

      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}

      tags:
        Name: default-rt
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | Route table ID |
| arn | Route table ARN |
| owner_id | AWS account ID |

## Best Practices

- **Use explicit associations** instead of main route table
- **Separate route tables** for public/private subnets
- **Document routes** with meaningful names
- **Use separate aws_route** for dynamic configurations
- **Plan CIDR ranges** to avoid overlaps
- **Test routing** before production deployment

## Troubleshooting

| Issue | Check |
|-------|-------|
| No internet access | IGW attached? Route to 0.0.0.0/0? |
| Private subnet no outbound | NAT Gateway? Route to NAT? |
| VPC peering not working | Routes in both VPCs? CIDR non-overlapping? |
| Asymmetric routing | Same path for request/response? |

## Related Resources

- [VPC](vpc.md)
- [Internet Gateway](internet-gateway.md)
- [Security Groups](security-groups.md)
