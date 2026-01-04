# VPC and Subnets

Create and manage Amazon VPC networks using ytofu YAML.

## Basic VPC

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
```

## VPC with Tags

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      instance_tenancy: default
      tags:
        Name: main
```

## VPC with CIDR from AWS IPAM

```yaml
data:
  aws_region:
    current: {}

resource:
  aws_vpc_ipam:
    test:
      operating_regions:
        - region_name: ${data.aws_region.current.region}

  aws_vpc_ipam_pool:
    test:
      address_family: ipv4
      ipam_scope_id: ${aws_vpc_ipam.test.private_default_scope_id}
      locale: ${data.aws_region.current.region}

  aws_vpc_ipam_pool_cidr:
    test:
      ipam_pool_id: ${aws_vpc_ipam_pool.test.id}
      cidr: 172.20.0.0/16

  aws_vpc:
    test:
      ipv4_ipam_pool_id: ${aws_vpc_ipam_pool.test.id}
      ipv4_netmask_length: 28
      depends_on:
        - aws_vpc_ipam_pool_cidr.test
```

## Arguments Reference (VPC)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| cidr_block | string | Yes* | Primary CIDR block |
| ipv4_ipam_pool_id | string | No | IPAM pool ID for CIDR |
| ipv4_netmask_length | number | No | Netmask length for IPAM |
| enable_dns_support | bool | No | Enable DNS resolution (default: true) |
| enable_dns_hostnames | bool | No | Enable DNS hostnames (default: false) |
| instance_tenancy | string | No | Tenancy: default, dedicated |
| tags | map | No | Resource tags |

*Required unless using IPAM

## Subnets

### Public Subnet

```yaml
resource:
  aws_subnet:
    public:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-subnet
        Type: public
```

### Private Subnet

```yaml
resource:
  aws_subnet:
    private:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.10.0/24
      availability_zone: us-west-2a
      tags:
        Name: private-subnet
        Type: private
```

## Arguments Reference (Subnet)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| vpc_id | string | Yes | VPC ID |
| cidr_block | string | Yes | Subnet CIDR block |
| availability_zone | string | No | AZ for the subnet |
| map_public_ip_on_launch | bool | No | Auto-assign public IPs |
| tags | map | No | Resource tags |

## Common Patterns

### Multi-AZ VPC with Public and Private Subnets

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      tags:
        Name: main-vpc

  # Public Subnets
  aws_subnet:
    public_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true
      tags:
        Name: public-a
        Type: public

    public_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.2.0/24
      availability_zone: us-west-2b
      map_public_ip_on_launch: true
      tags:
        Name: public-b
        Type: public

  # Private Subnets
    private_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.10.0/24
      availability_zone: us-west-2a
      tags:
        Name: private-a
        Type: private

    private_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.11.0/24
      availability_zone: us-west-2b
      tags:
        Name: private-b
        Type: private

  # Internet Gateway
  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-igw

  # Public Route Table
  aws_route_table:
    public:
      vpc_id: ${aws_vpc.main.id}
      route:
        - cidr_block: 0.0.0.0/0
          gateway_id: ${aws_internet_gateway.main.id}
      tags:
        Name: public-rt

  # Associate Public Subnets
  aws_route_table_association:
    public_a:
      subnet_id: ${aws_subnet.public_a.id}
      route_table_id: ${aws_route_table.public.id}

    public_b:
      subnet_id: ${aws_subnet.public_b.id}
      route_table_id: ${aws_route_table.public.id}
```

### VPC with Secondary CIDR

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      tags:
        Name: main-vpc

  aws_vpc_ipv4_cidr_block_association:
    secondary:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.1.0.0/16
```

### VPC with IPv6

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      assign_generated_ipv6_cidr_block: true
      tags:
        Name: main-vpc

  aws_subnet:
    public:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      ipv6_cidr_block: ${cidrsubnet(aws_vpc.main.ipv6_cidr_block, 8, 1)}
      assign_ipv6_address_on_creation: true
```

## Attributes Reference

### VPC

| Attribute | Description |
|-----------|-------------|
| id | VPC ID |
| arn | VPC ARN |
| default_route_table_id | Default route table ID |
| default_security_group_id | Default security group ID |
| ipv6_cidr_block | IPv6 CIDR block (if enabled) |

### Subnet

| Attribute | Description |
|-----------|-------------|
| id | Subnet ID |
| arn | Subnet ARN |
| availability_zone_id | AZ ID |

## Best Practices

- **Plan CIDR ranges carefully** - Leave room for growth
- **Use /16 for VPC** and /24 for subnets
- **Deploy across multiple AZs** for high availability
- **Separate public and private subnets** by function
- **Use consistent naming** and tagging conventions
- **Reserve IP space** for future expansion
- **Enable VPC Flow Logs** for troubleshooting

## CIDR Planning Example

```
VPC: 10.0.0.0/16 (65,536 IPs)
├── Public Subnets (10.0.0.0/20)
│   ├── 10.0.0.0/24 - public-a (256 IPs)
│   ├── 10.0.1.0/24 - public-b (256 IPs)
│   └── 10.0.2.0/24 - public-c (256 IPs)
├── Private Subnets (10.0.16.0/20)
│   ├── 10.0.16.0/24 - private-a (256 IPs)
│   ├── 10.0.17.0/24 - private-b (256 IPs)
│   └── 10.0.18.0/24 - private-c (256 IPs)
└── Database Subnets (10.0.32.0/20)
    ├── 10.0.32.0/24 - database-a (256 IPs)
    ├── 10.0.33.0/24 - database-b (256 IPs)
    └── 10.0.34.0/24 - database-c (256 IPs)
```

## Related Resources

- [Security Groups](security-groups.md)
- [Internet Gateway](internet-gateway.md)
- [Route Tables](route-tables.md)
- [EC2 Instance](../compute/ec2-instance.md)
