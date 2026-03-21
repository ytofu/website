# OpenSearch VPC Endpoint

Create VPC endpoints for OpenSearch domains using ytofu YAML.

## Basic Endpoint

```yaml
resource:
  aws_opensearch_vpc_endpoint:
    example:
      domain_arn: ${aws_opensearch_domain.example.arn}
      vpc_options:
        security_group_ids:
          - ${aws_security_group.example.id}
        subnet_ids:
          - ${aws_subnet.example.id}
```
