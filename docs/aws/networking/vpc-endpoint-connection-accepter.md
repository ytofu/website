# VPC Endpoint Connection Accepter

Manage VPC Endpoint Connection Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_service:
    example:
      acceptance_required: false
      network_load_balancer_arns: 
        - ${aws_lb.example.arn}

resource:
  aws_vpc_endpoint:
    example:
      vpc_id: ${aws_vpc.test_alternate.id}
      service_name: ${aws_vpc_endpoint_service.test.service_name}
      vpc_endpoint_type: Interface
      private_dns_enabled: false
      security_group_ids:
        - ${aws_security_group.test.id}

resource:
  aws_vpc_endpoint_connection_accepter:
    example:
      vpc_endpoint_service_id: ${aws_vpc_endpoint_service.example.id}
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
```
