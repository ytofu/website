# AWS Networking

Build and manage AWS network infrastructure with ytofu YAML.

## Overview

AWS networking provides the foundation for all cloud resources:

| Resource | Purpose |
|----------|---------|
| [VPC](vpc.md) | Isolated virtual network |
| [Security Groups](security-groups.md) | Instance-level firewall |
| [Internet Gateway](internet-gateway.md) | Public internet access |
| [Load Balancer](load-balancer.md) | Traffic distribution |
| [Route Tables](route-tables.md) | Network routing |
| [Route53](route53.md) | DNS management |

## Quick Start: Complete VPC

```yaml
resource:
  # VPC
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
      enable_dns_hostnames: true
      tags:
        Name: main-vpc

  # Public Subnet
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
      cidr_block: 10.0.2.0/24
      availability_zone: us-west-2a
      tags:
        Name: private-subnet

  # Internet Gateway
  aws_internet_gateway:
    main:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main-igw

  # Security Group
  aws_security_group:
    web:
      name: web-sg
      vpc_id: ${aws_vpc.main.id}
      description: Allow HTTP/HTTPS

      ingress:
        - from_port: 80
          to_port: 80
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0

        - from_port: 443
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
```

## Network Architecture Patterns

### Public + Private Subnets

```
┌─────────────────────────────────────────┐
│                   VPC                   │
│  ┌─────────────┐    ┌─────────────┐    │
│  │   Public    │    │   Private   │    │
│  │   Subnet    │    │   Subnet    │    │
│  │  (10.0.1.0) │    │  (10.0.2.0) │    │
│  │      │      │    │      │      │    │
│  │   [Web]     │    │   [DB]      │    │
│  └──────┼──────┘    └──────┼──────┘    │
│         │                  │           │
│    ┌────┴────┐        ┌────┴────┐      │
│    │   IGW   │        │   NAT   │      │
│    └────┬────┘        └────┬────┘      │
└─────────┼──────────────────┼───────────┘
          │                  │
       Internet           Internet
       (inbound)          (outbound)
```

### Multi-AZ High Availability

```yaml
resource:
  aws_subnet:
    public_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      map_public_ip_on_launch: true

    public_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.2.0/24
      availability_zone: us-west-2b
      map_public_ip_on_launch: true

    public_c:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.3.0/24
      availability_zone: us-west-2c
      map_public_ip_on_launch: true
```

## Best Practices

- **Use multiple AZs** for high availability
- **Separate public and private subnets** for security
- **Use NAT Gateway** for private subnet internet access
- **Apply least-privilege security groups**
- **Enable VPC Flow Logs** for network monitoring
- **Use VPC Endpoints** for AWS service access without internet

## Related Resources

- [EC2 Instance](../compute/ec2-instance.md)
- [Load Balancer](load-balancer.md)
- [ECS](../compute/ecs.md)
