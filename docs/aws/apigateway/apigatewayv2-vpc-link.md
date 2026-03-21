# Apigatewayv2 VPC Link

Manage Apigatewayv2 VPC Link resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_vpc_link:
    example:
      name: example
      security_group_ids: 
        - ${data.aws_security_group.example.id}
      subnet_ids: ${data.aws_subnets.example.ids}
      tags:
        Usage: example
```
