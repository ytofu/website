# VPC Endpoint Service Allowed Principal

Manage VPC Endpoint Service Allowed Principal resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_vpc_endpoint_service_allowed_principal:
    allow_me_to_foo:
      vpc_endpoint_service_id: ${aws_vpc_endpoint_service.foo.id}
      principal_arn: ${data.aws_caller_identity.current.arn}
```
