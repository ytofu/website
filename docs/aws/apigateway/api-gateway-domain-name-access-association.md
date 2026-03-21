# API Gateway Domain Name Access Association

Manage API Gateway Domain Name Access Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_domain_name_access_association:
    example:
      access_association_source: ${aws_vpc_endpoint.example.id}
      access_association_source_type: VPCE
      domain_name_arn: ${aws_api_gateway_domain_name.example.arn}
```
