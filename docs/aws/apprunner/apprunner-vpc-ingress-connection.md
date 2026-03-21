# Apprunner VPC Ingress Connection

Manage Apprunner VPC Ingress Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_vpc_ingress_connection:
    example:
      name: example
      service_arn: ${aws_apprunner_service.example.arn}
      ingress_vpc_configuration:
        vpc_id: ${aws_default_vpc.default.id}
        vpc_endpoint_id: ${aws_vpc_endpoint.apprunner.id}
      tags:
        foo: bar
```
