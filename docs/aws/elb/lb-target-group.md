# LB Target Group

Manage LB Target Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lb_target_group:
    test:
      name: tf-example-lb-tg
      port: 80
      protocol: HTTP
      vpc_id: ${aws_vpc.main.id}

resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
```

## IP Target Group

```yaml
resource:
  aws_lb_target_group:
    ip-example:
      name: tf-example-lb-tg
      port: 80
      protocol: HTTP
      target_type: ip
      vpc_id: ${aws_vpc.main.id}

resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
```

## Lambda Target Group

```yaml
resource:
  aws_lb_target_group:
    lambda-example:
      name: tf-example-lb-tg
      target_type: lambda
```

## ALB Target Group

```yaml
resource:
  aws_lb_target_group:
    alb-example:
      name: tf-example-lb-alb-tg
      target_type: alb
      port: 80
      protocol: TCP
      vpc_id: ${aws_vpc.main.id}
```

## Target group with unhealthy connection termination disabled

```yaml
resource:
  aws_lb_target_group:
    tcp-example:
      name: tf-example-lb-nlb-tg
      port: 25
      protocol: TCP
      vpc_id: ${aws_vpc.main.id}
      target_health_state:
        enable_unhealthy_connection_termination: false
```

## Target group with health requirements

```yaml
resource:
  aws_lb_target_group:
    tcp-example:
      name: tf-example-lb-nlb-tg
      port: 80
      protocol: TCP
      vpc_id: ${aws_vpc.main.id}
      target_group_health:
        dns_failover:
          minimum_healthy_targets_count: 1
          minimum_healthy_targets_percentage: off
        unhealthy_state_routing:
          minimum_healthy_targets_count: 1
          minimum_healthy_targets_percentage: off
```
