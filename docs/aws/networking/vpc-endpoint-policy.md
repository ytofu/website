# VPC Endpoint Policy

Manage VPC Endpoint Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_vpc_endpoint_service:
    example:
      service: dynamodb

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpc_endpoint:
    example:
      service_name: ${data.aws_vpc_endpoint_service.example.service_name}
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_vpc_endpoint_policy:
    example:
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
      policy: '{ "Version" : "2012-10-17", "Statement" : [ { "Sid" : "AllowAll", "Effect" : "Allow", "Principal" : { "AWS" : "*" }, "Action" : [ "dynamodb:*" ], "Resource" : "*" } ] }'
```
