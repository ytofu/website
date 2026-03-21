# VPC Endpoint Service Private DNS Verification

Manage VPC Endpoint Service Private DNS Verification resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_service_private_dns_verification:
    example:
      service_id: ${aws_vpc_endpoint_service.example.id}
```
