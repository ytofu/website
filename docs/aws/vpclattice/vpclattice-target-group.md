# Vpclattice Target Group

Manage Vpclattice Target Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_target_group:
    example:
      name: example
      type: INSTANCE
      config:
        vpc_identifier: ${aws_vpc.example.id}
        port: 443
        protocol: HTTPS
```

## Basic usage with Health check

```yaml
resource:
  aws_vpclattice_target_group:
    example:
      name: example
      type: IP
      config:
        vpc_identifier: ${aws_vpc.example.id}
        ip_address_type: IPV4
        port: 443
        protocol: HTTPS
        protocol_version: HTTP1
        health_check:
          enabled: true
          health_check_interval_seconds: 20
          health_check_timeout_seconds: 10
          healthy_threshold_count: 7
          unhealthy_threshold_count: 3
          matcher:
            value: 200-299
          path: /instance
          port: 80
          protocol: HTTP
          protocol_version: HTTP1
```

## ALB

```yaml
resource:
  aws_vpclattice_target_group:
    example:
      name: example
      type: ALB
      config:
        vpc_identifier: ${aws_vpc.example.id}
        port: 443
        protocol: HTTPS
        protocol_version: HTTP1
```

## Lambda

```yaml
resource:
  aws_vpclattice_target_group:
    example:
      name: example
      type: LAMBDA
```
