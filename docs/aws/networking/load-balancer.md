# Load Balancer

Deploy Application and Network Load Balancers using ytofu YAML.

## Application Load Balancer

```yaml
resource:
  aws_lb:
    test:
      name: test-lb-tf
      internal: false
      load_balancer_type: application
      security_groups:
        - ${aws_security_group.lb_sg.id}
      subnets:
        - ${aws_subnet.public_a.id}
        - ${aws_subnet.public_b.id}
      enable_deletion_protection: true
      access_logs:
        bucket: ${aws_s3_bucket.lb_logs.id}
        prefix: test-lb
        enabled: true
      tags:
        Environment: production
```

## Network Load Balancer

```yaml
resource:
  aws_lb:
    test:
      name: test-lb-tf
      internal: false
      load_balancer_type: network
      subnets:
        - ${aws_subnet.public_a.id}
        - ${aws_subnet.public_b.id}
      enable_deletion_protection: true
      tags:
        Environment: production
```

## Elastic IP Assignment

```yaml
resource:
  aws_lb:
    example:
      name: example
      load_balancer_type: network
      subnet_mapping:
        - subnet_id: ${aws_subnet.example1.id}
          allocation_id: ${aws_eip.example1.id}
        - subnet_id: ${aws_subnet.example2.id}
          allocation_id: ${aws_eip.example2.id}
```

## Private IP Addresses for Internal Load Balancer

```yaml
resource:
  aws_lb:
    example:
      name: example
      load_balancer_type: network
      subnet_mapping:
        - subnet_id: ${aws_subnet.example1.id}
          private_ipv4_address: 10.0.1.15
        - subnet_id: ${aws_subnet.example2.id}
          private_ipv4_address: 10.0.2.15
```

## Arguments Reference (Load Balancer)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | No | Load balancer name |
| internal | bool | No | Internal LB (default: false) |
| load_balancer_type | string | No | "application" or "network" |
| security_groups | list | No | Security group IDs (ALB only) |
| subnets | list | Yes* | Subnet IDs |
| subnet_mapping | list | No | Subnet mapping with IPs |
| enable_deletion_protection | bool | No | Prevent deletion |
| access_logs | object | No | S3 access logs config |
| tags | map | No | Resource tags |

*Required unless using subnet_mapping

## Complete ALB Setup

```yaml
resource:
  # Application Load Balancer
  aws_lb:
    main:
      name: my-alb
      internal: false
      load_balancer_type: application
      security_groups:
        - ${aws_security_group.alb.id}
      subnets:
        - ${aws_subnet.public_a.id}
        - ${aws_subnet.public_b.id}
      enable_deletion_protection: false
      tags:
        Name: my-alb

  # Target Group
  aws_lb_target_group:
    app:
      name: app-tg
      port: 8080
      protocol: HTTP
      vpc_id: ${aws_vpc.main.id}
      target_type: instance
      health_check:
        enabled: true
        path: /health
        port: traffic-port
        protocol: HTTP
        healthy_threshold: 2
        unhealthy_threshold: 3
        timeout: 5
        interval: 30
      tags:
        Name: app-tg

  # HTTP Listener (redirect to HTTPS)
  aws_lb_listener:
    http:
      load_balancer_arn: ${aws_lb.main.arn}
      port: 80
      protocol: HTTP
      default_action:
        - type: redirect
          redirect:
            port: "443"
            protocol: HTTPS
            status_code: HTTP_301

  # HTTPS Listener
  aws_lb_listener:
    https:
      load_balancer_arn: ${aws_lb.main.arn}
      port: 443
      protocol: HTTPS
      ssl_policy: ELBSecurityPolicy-TLS13-1-2-2021-06
      certificate_arn: ${aws_acm_certificate.main.arn}
      default_action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.app.arn}
```

## Arguments Reference (Target Group)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | No | Target group name |
| port | number | Yes | Target port |
| protocol | string | Yes | HTTP, HTTPS, TCP, UDP |
| vpc_id | string | Yes | VPC ID |
| target_type | string | No | instance, ip, lambda |
| health_check | object | No | Health check config |
| tags | map | No | Resource tags |

## Common Patterns

### ALB with Path-Based Routing

```yaml
resource:
  aws_lb_target_group:
    api:
      name: api-tg
      port: 8080
      protocol: HTTP
      vpc_id: ${aws_vpc.main.id}

    web:
      name: web-tg
      port: 3000
      protocol: HTTP
      vpc_id: ${aws_vpc.main.id}

  aws_lb_listener:
    https:
      load_balancer_arn: ${aws_lb.main.arn}
      port: 443
      protocol: HTTPS
      certificate_arn: ${aws_acm_certificate.main.arn}
      default_action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.web.arn}

  aws_lb_listener_rule:
    api:
      listener_arn: ${aws_lb_listener.https.arn}
      priority: 100
      action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.api.arn}
      condition:
        - path_pattern:
            values:
              - /api/*
```

### ALB with Host-Based Routing

```yaml
resource:
  aws_lb_listener_rule:
    app1:
      listener_arn: ${aws_lb_listener.https.arn}
      priority: 100
      action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.app1.arn}
      condition:
        - host_header:
            values:
              - app1.example.com

    app2:
      listener_arn: ${aws_lb_listener.https.arn}
      priority: 200
      action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.app2.arn}
      condition:
        - host_header:
            values:
              - app2.example.com
```

### ALB with Weighted Target Groups

```yaml
resource:
  aws_lb_listener:
    https:
      load_balancer_arn: ${aws_lb.main.arn}
      port: 443
      protocol: HTTPS
      certificate_arn: ${aws_acm_certificate.main.arn}
      default_action:
        - type: forward
          forward:
            target_group:
              - arn: ${aws_lb_target_group.blue.arn}
                weight: 90
              - arn: ${aws_lb_target_group.green.arn}
                weight: 10
            stickiness:
              enabled: true
              duration: 3600
```

## Network Load Balancer with TLS

```yaml
resource:
  aws_lb:
    nlb:
      name: my-nlb
      internal: false
      load_balancer_type: network
      subnets:
        - ${aws_subnet.public_a.id}
        - ${aws_subnet.public_b.id}
      enable_cross_zone_load_balancing: true
      tags:
        Name: my-nlb

  aws_lb_target_group:
    tcp:
      name: tcp-tg
      port: 443
      protocol: TCP
      vpc_id: ${aws_vpc.main.id}
      health_check:
        protocol: TCP
        port: traffic-port

  aws_lb_listener:
    tls:
      load_balancer_arn: ${aws_lb.nlb.arn}
      port: 443
      protocol: TLS
      certificate_arn: ${aws_acm_certificate.main.arn}
      ssl_policy: ELBSecurityPolicy-TLS13-1-2-2021-06
      default_action:
        - type: forward
          target_group_arn: ${aws_lb_target_group.tcp.arn}
```

## Target Registration

### Register EC2 Instances

```yaml
resource:
  aws_lb_target_group_attachment:
    web1:
      target_group_arn: ${aws_lb_target_group.app.arn}
      target_id: ${aws_instance.web1.id}
      port: 8080

    web2:
      target_group_arn: ${aws_lb_target_group.app.arn}
      target_id: ${aws_instance.web2.id}
      port: 8080
```

### IP-Based Targets (for ECS/Fargate)

```yaml
resource:
  aws_lb_target_group:
    ecs:
      name: ecs-tg
      port: 8080
      protocol: HTTP
      vpc_id: ${aws_vpc.main.id}
      target_type: ip
      health_check:
        path: /health
        matcher: "200"
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | Load balancer ID |
| arn | Load balancer ARN |
| arn_suffix | ARN suffix for CloudWatch |
| dns_name | DNS name |
| zone_id | Route53 zone ID |

## Best Practices

- **Use HTTPS** with valid certificates
- **Enable access logs** for troubleshooting
- **Configure health checks** appropriately
- **Use multiple AZs** for high availability
- **Enable deletion protection** for production
- **Use appropriate SSL policies**
- **Monitor with CloudWatch**

## ALB vs NLB

| Feature | ALB | NLB |
|---------|-----|-----|
| Layer | 7 (HTTP/HTTPS) | 4 (TCP/UDP) |
| Routing | Path, host, header | Port-based |
| Performance | Good | Ultra-low latency |
| Static IP | No | Yes |
| WebSocket | Yes | Yes |
| gRPC | Yes | No |

## Related Resources

- [Security Groups](security-groups.md)
- [VPC](vpc.md)
- [Route53](route53.md)
- [EC2 Instance](../compute/ec2-instance.md)
- [ECS](../compute/ecs.md)
