# Internet Gateway

An Internet Gateway allows public subnets to communicate with the internet.

## Basic Example

```yaml
resource:
  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-igw
```

## With Route Table

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      tags:
        Name: main-vpc

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

  aws_subnet:
    public:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet

  aws_route_table_association:
    public:
      subnet_id: ${aws_subnet.public.id}
      route_table_id: ${aws_route_table.public.id}
```

## Arguments Reference

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| vpc_id | string | Yes | VPC to attach to |
| tags | map | No | Resource tags |

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | Internet Gateway ID |
| arn | Internet Gateway ARN |
| owner_id | AWS account ID |

## Cost Considerations

| Resource | Pricing |
|----------|---------|
| Internet Gateway | Free |

## Best Practices

- **One IGW per VPC** - Each VPC can only have one Internet Gateway
- **Attach before creating public routes** - Ensure IGW is attached before adding routes
- **Use with public subnets only** - Private subnets should use NAT Gateway instead
- **Tag for identification** - Use meaningful tags for resource management

## Troubleshooting

| Issue | Solution |
|-------|----------|
| No internet from public subnet | Check IGW route and public IP assignment |
| Cannot attach IGW | Ensure VPC doesn't already have an IGW |
| Route table not working | Verify route table is associated with subnet |

## Related Resources

- [NAT Gateway](nat-gateway.md)
- [VPC](vpc.md)
- [Route Tables](route-tables.md)
- [Security Groups](security-groups.md)
