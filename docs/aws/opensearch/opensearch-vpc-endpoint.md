# Opensearch VPC Endpoint

Manage Opensearch VPC Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearch_vpc_endpoint:
    foo:
      domain_arn: ${aws_opensearch_domain.domain_1.arn}
      vpc_options:
        security_group_ids: 
          - ${aws_security_group.test.id}
          - ${aws_security_group.test2.id}
        subnet_ids: 
          - ${aws_subnet.test.id}
          - ${aws_subnet.test2.id}
```
