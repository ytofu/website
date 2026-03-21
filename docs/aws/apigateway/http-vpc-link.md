# API Gateway v2 VPC Link

Create VPC links for HTTP API private integrations using ytofu YAML.

## Basic VPC Link

```yaml
resource:
  aws_apigatewayv2_vpc_link:
    example:
      name: example
      security_group_ids:
        - ${aws_security_group.example.id}
      subnet_ids: ${aws_subnet.example[*].id}
```
