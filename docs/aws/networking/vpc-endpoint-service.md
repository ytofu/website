# VPC Endpoint Service

Manage VPC Endpoint Service resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_service:
    example:
      acceptance_required: false
      network_load_balancer_arns: 
        - ${aws_lb.example.arn}
```

## Gateway Load Balancers

```yaml
resource:
  aws_vpc_endpoint_service:
    example:
      acceptance_required: false
      gateway_load_balancer_arns: 
        - ${aws_lb.example.arn}
```
