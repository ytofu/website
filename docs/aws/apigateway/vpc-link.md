# API Gateway VPC Link

Create VPC links for private integrations using ytofu YAML.

## REST API VPC Link

```yaml
resource:
  aws_api_gateway_vpc_link:
    example:
      name: example
      description: VPC link for NLB
      target_arns:
        - ${aws_lb.example.arn}
```
