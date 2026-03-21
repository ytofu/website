# VPC Endpoint Private DNS

Manage VPC Endpoint Private DNS resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_private_dns:
    example:
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
      private_dns_enabled: true
```
