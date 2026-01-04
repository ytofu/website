# Security Groups

Create and manage AWS Security Groups using ytofu YAML.

## Basic Example with Separate Rules (Recommended)

```yaml
resource:
  aws_security_group:
    allow_tls:
      name: allow_tls
      description: Allow TLS inbound traffic and all outbound traffic
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: allow_tls

  aws_vpc_security_group_ingress_rule:
    allow_tls_ipv4:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv4: ${aws_vpc.main.cidr_block}
      from_port: 443
      ip_protocol: tcp
      to_port: 443

    allow_tls_ipv6:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv6: ${aws_vpc.main.ipv6_cidr_block}
      from_port: 443
      ip_protocol: tcp
      to_port: 443

  aws_vpc_security_group_egress_rule:
    allow_all_traffic_ipv4:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1"

    allow_all_traffic_ipv6:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv6: "::/0"
      ip_protocol: "-1"
```

## Inline Rules (Legacy Style)

```yaml
resource:
  aws_security_group:
    example:
      name: example-sg
      vpc_id: ${aws_vpc.main.id}
      description: Example security group

      ingress:
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
          ipv6_cidr_blocks:
            - "::/0"
```

## With Prefix List IDs

```yaml
resource:
  aws_security_group:
    example:
      name: example-sg
      vpc_id: ${aws_vpc.main.id}

      egress:
        - from_port: 0
          to_port: 0
          protocol: "-1"
          prefix_list_ids:
            - ${aws_vpc_endpoint.my_endpoint.prefix_list_id}
```

## Removing All Rules

```yaml
resource:
  aws_security_group:
    example:
      name: sg
      vpc_id: ${aws_vpc.example.id}
      ingress: []
      egress: []
```

## Create Before Destroy

```yaml
resource:
  aws_security_group:
    example:
      name: changeable-name
      vpc_id: ${aws_vpc.main.id}
      lifecycle:
        create_before_destroy: true
```

## Arguments Reference

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | No | Security group name |
| name_prefix | string | No | Name prefix (for unique names) |
| vpc_id | string | Yes | VPC ID |
| description | string | No | Security group description |
| ingress | list | No | Inbound rules (inline) |
| egress | list | No | Outbound rules (inline) |
| tags | map | No | Resource tags |

### Ingress/Egress Rule Arguments

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| from_port | number | Yes | Start port |
| to_port | number | Yes | End port |
| protocol | string | Yes | Protocol (tcp, udp, icmp, -1 for all) |
| cidr_blocks | list | No | IPv4 CIDR blocks |
| ipv6_cidr_blocks | list | No | IPv6 CIDR blocks |
| security_groups | list | No | Source/dest security group IDs |
| prefix_list_ids | list | No | VPC endpoint prefix list IDs |
| self | bool | No | Allow traffic from same SG |
| description | string | No | Rule description |

## Common Patterns

### Web Server (HTTP/HTTPS)

```yaml
resource:
  aws_security_group:
    web:
      name: web-sg
      vpc_id: ${aws_vpc.main.id}
      description: Web server security group
      tags:
        Name: web-sg

  aws_vpc_security_group_ingress_rule:
    http:
      security_group_id: ${aws_security_group.web.id}
      cidr_ipv4: 0.0.0.0/0
      from_port: 80
      to_port: 80
      ip_protocol: tcp
      description: HTTP

    https:
      security_group_id: ${aws_security_group.web.id}
      cidr_ipv4: 0.0.0.0/0
      from_port: 443
      to_port: 443
      ip_protocol: tcp
      description: HTTPS

  aws_vpc_security_group_egress_rule:
    all_outbound:
      security_group_id: ${aws_security_group.web.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1"
```

### Database (Private Access Only)

```yaml
resource:
  aws_security_group:
    database:
      name: database-sg
      vpc_id: ${aws_vpc.main.id}
      description: Database security group
      tags:
        Name: database-sg

  aws_vpc_security_group_ingress_rule:
    postgres_from_app:
      security_group_id: ${aws_security_group.database.id}
      referenced_security_group_id: ${aws_security_group.app.id}
      from_port: 5432
      to_port: 5432
      ip_protocol: tcp
      description: PostgreSQL from app servers

  aws_vpc_security_group_egress_rule:
    all_outbound:
      security_group_id: ${aws_security_group.database.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1"
```

### Application with Multiple Tiers

```yaml
resource:
  # Load Balancer SG
  aws_security_group:
    alb:
      name: alb-sg
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: alb-sg

  aws_vpc_security_group_ingress_rule:
    alb_http:
      security_group_id: ${aws_security_group.alb.id}
      cidr_ipv4: 0.0.0.0/0
      from_port: 80
      to_port: 80
      ip_protocol: tcp

    alb_https:
      security_group_id: ${aws_security_group.alb.id}
      cidr_ipv4: 0.0.0.0/0
      from_port: 443
      to_port: 443
      ip_protocol: tcp

  aws_vpc_security_group_egress_rule:
    alb_all:
      security_group_id: ${aws_security_group.alb.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1"

  # Application SG
  aws_security_group:
    app:
      name: app-sg
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: app-sg

  aws_vpc_security_group_ingress_rule:
    app_from_alb:
      security_group_id: ${aws_security_group.app.id}
      referenced_security_group_id: ${aws_security_group.alb.id}
      from_port: 8080
      to_port: 8080
      ip_protocol: tcp
      description: Traffic from ALB

  aws_vpc_security_group_egress_rule:
    app_all:
      security_group_id: ${aws_security_group.app.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1"

  # Database SG
  aws_security_group:
    db:
      name: db-sg
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: db-sg

  aws_vpc_security_group_ingress_rule:
    db_from_app:
      security_group_id: ${aws_security_group.db.id}
      referenced_security_group_id: ${aws_security_group.app.id}
      from_port: 3306
      to_port: 3306
      ip_protocol: tcp
      description: MySQL from app

  aws_vpc_security_group_egress_rule:
    db_all:
      security_group_id: ${aws_security_group.db.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1"
```

### ECS/Container Security Group

```yaml
resource:
  aws_security_group:
    ecs_tasks:
      name: ecs-tasks-sg
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: ecs-tasks-sg

  aws_vpc_security_group_ingress_rule:
    ecs_from_alb:
      security_group_id: ${aws_security_group.ecs_tasks.id}
      referenced_security_group_id: ${aws_security_group.alb.id}
      from_port: 0
      to_port: 65535
      ip_protocol: tcp
      description: Allow from ALB

    ecs_internal:
      security_group_id: ${aws_security_group.ecs_tasks.id}
      referenced_security_group_id: ${aws_security_group.ecs_tasks.id}
      from_port: 0
      to_port: 65535
      ip_protocol: tcp
      description: Allow internal communication

  aws_vpc_security_group_egress_rule:
    ecs_all:
      security_group_id: ${aws_security_group.ecs_tasks.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1"
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | Security group ID |
| arn | Security group ARN |
| owner_id | AWS account ID |

## Best Practices

- **Use separate rule resources** (`aws_vpc_security_group_ingress_rule`) instead of inline rules
- **Use descriptive names** and descriptions for rules
- **Follow least privilege** - Only open required ports
- **Reference security groups** instead of CIDR when possible
- **Avoid 0.0.0.0/0** for ingress except for public endpoints
- **Use separate SGs** for different tiers (web, app, db)
- **Use create_before_destroy** for name changes
- **Review regularly** for unused or overly permissive rules

## Common Port Reference

| Port | Service |
|------|---------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 27017 | MongoDB |
| 8080 | HTTP Alt |

## Related Resources

- [VPC](vpc.md)
- [EC2 Instance](../compute/ec2-instance.md)
- [Load Balancer](load-balancer.md)
- [ECS](../compute/ecs.md)
