# Blue/Green Deployment

Implement zero-downtime deployments with traffic shifting.

## Problem

You need to deploy new versions of your application without downtime and with the ability to quickly rollback if issues are detected.

## Solution

Maintain two identical environments (blue and green), deploy to the inactive environment, then shift traffic.

## Architecture

```
                         Route53 / ALB
                              │
              ┌───────────────┼───────────────┐
              │               │               │
              ▼               │               ▼
       ┌─────────────┐        │        ┌─────────────┐
       │    Blue     │        │        │    Green    │
       │  (Current)  │◄───────┴───────►│   (New)     │
       │   v1.0.0    │    Traffic      │   v1.1.0    │
       └─────────────┘    Shifting     └─────────────┘
```

## Deployment Flow

1. **Blue is live** - Serving 100% of traffic
2. **Deploy to Green** - Deploy new version
3. **Test Green** - Validate new version
4. **Shift traffic** - Gradually move traffic to Green
5. **Green is live** - Blue becomes standby
6. **Rollback if needed** - Shift traffic back to Blue

## Configuration

### Using ALB with Weighted Target Groups

```yaml
resource:
  # Blue Target Group
  aws_lb_target_group:
    blue:
      name: app-blue-tg
      port: 80
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
        Name: app-blue-tg
        Environment: blue

  # Green Target Group
  aws_lb_target_group:
    green:
      name: app-green-tg
      port: 80
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
        Name: app-green-tg
        Environment: green

  # ALB Listener with Weighted Routing
  aws_lb_listener:
    https:
      load_balancer_arn: ${aws_lb.main.arn}
      port: 443
      protocol: HTTPS
      ssl_policy: ELBSecurityPolicy-TLS13-1-2-2021-06
      certificate_arn: ${aws_acm_certificate.main.arn}
      default_action:
        - type: forward
          forward:
            target_group:
              - arn: ${aws_lb_target_group.blue.arn}
                weight: 100
              - arn: ${aws_lb_target_group.green.arn}
                weight: 0
            stickiness:
              enabled: true
              duration: 3600
```

### Traffic Shifting Stages

**Stage 1: 100% Blue (Initial)**
```yaml
target_group:
  - arn: ${aws_lb_target_group.blue.arn}
    weight: 100
  - arn: ${aws_lb_target_group.green.arn}
    weight: 0
```

**Stage 2: Canary (10% Green)**
```yaml
target_group:
  - arn: ${aws_lb_target_group.blue.arn}
    weight: 90
  - arn: ${aws_lb_target_group.green.arn}
    weight: 10
```

**Stage 3: 50/50 Split**
```yaml
target_group:
  - arn: ${aws_lb_target_group.blue.arn}
    weight: 50
  - arn: ${aws_lb_target_group.green.arn}
    weight: 50
```

**Stage 4: 100% Green (Complete)**
```yaml
target_group:
  - arn: ${aws_lb_target_group.blue.arn}
    weight: 0
  - arn: ${aws_lb_target_group.green.arn}
    weight: 100
```

### Using Route53 Weighted Routing

Alternative approach using DNS-level traffic splitting:

```yaml
resource:
  aws_route53_record:
    blue:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: blue

      alias:
        name: ${aws_lb.blue.dns_name}
        zone_id: ${aws_lb.blue.zone_id}
        evaluate_target_health: true

      weighted_routing_policy:
        weight: 100

    green:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: green

      alias:
        name: ${aws_lb.green.dns_name}
        zone_id: ${aws_lb.green.zone_id}
        evaluate_target_health: true

      weighted_routing_policy:
        weight: 0
```

### ECS Blue/Green with CodeDeploy

For ECS, use CodeDeploy for automated blue/green:

```yaml
resource:
  aws_codedeploy_app:
    main:
      compute_platform: ECS
      name: web-app

  aws_codedeploy_deployment_group:
    main:
      app_name: ${aws_codedeploy_app.main.name}
      deployment_config_name: CodeDeployDefault.ECSLinear10PercentEvery1Minutes
      deployment_group_name: web-app-dg
      service_role_arn: ${aws_iam_role.codedeploy.arn}

      auto_rollback_configuration:
        enabled: true
        events:
          - DEPLOYMENT_FAILURE

      blue_green_deployment_config:
        deployment_ready_option:
          action_on_timeout: CONTINUE_DEPLOYMENT
          wait_time_in_minutes: 0

        terminate_blue_instances_on_deployment_success:
          action: TERMINATE
          termination_wait_time_in_minutes: 5

      deployment_style:
        deployment_option: WITH_TRAFFIC_CONTROL
        deployment_type: BLUE_GREEN

      ecs_service:
        cluster_name: ${aws_ecs_cluster.main.name}
        service_name: ${aws_ecs_service.main.name}

      load_balancer_info:
        target_group_pair_info:
          prod_traffic_route:
            listener_arns:
              - ${aws_lb_listener.https.arn}

          target_group:
            - name: ${aws_lb_target_group.blue.name}
            - name: ${aws_lb_target_group.green.name}
```

## Deployment Strategies

| Strategy | Description | Risk | Speed |
|----------|-------------|------|-------|
| Linear 10% every minute | Gradual shift | Low | Slow |
| Linear 25% every 5 min | Balanced | Medium | Medium |
| Canary 10% then 100% | Quick validation | Medium | Fast |
| All at once | Immediate switch | High | Instant |

## Rollback

### Manual Rollback

Simply swap the weights back:

```yaml
# Rollback to Blue
target_group:
  - arn: ${aws_lb_target_group.blue.arn}
    weight: 100
  - arn: ${aws_lb_target_group.green.arn}
    weight: 0
```

### Automatic Rollback with CloudWatch

```yaml
resource:
  aws_cloudwatch_metric_alarm:
    high_error_rate:
      alarm_name: high-error-rate
      comparison_operator: GreaterThanThreshold
      evaluation_periods: 2
      metric_name: HTTPCode_Target_5XX_Count
      namespace: AWS/ApplicationELB
      period: 60
      statistic: Sum
      threshold: 10
      alarm_description: High 5XX error rate
      dimensions:
        LoadBalancer: ${aws_lb.main.arn_suffix}
        TargetGroup: ${aws_lb_target_group.green.arn_suffix}
```

## Best Practices

- **Always have health checks** - Ensure unhealthy targets don't receive traffic
- **Start with small percentages** - 5-10% canary to detect issues early
- **Monitor error rates** - Watch for increased 5XX errors during shift
- **Keep blue running** - Don't terminate blue until green is stable
- **Automate rollback** - Use CloudWatch alarms to trigger automatic rollback
- **Test in staging first** - Validate the process before production

## Related Resources

- [Load Balancer Reference](../aws/networking/load-balancer.md)
- [Route53 Reference](../aws/networking/route53.md)
- [ECS Reference](../aws/compute/ecs.md)
- [Multi-AZ Deployment](multi-az-deployment.md)
