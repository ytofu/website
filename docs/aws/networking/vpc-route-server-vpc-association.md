# VPC Route Server VPC Association

Manage VPC Route Server VPC Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_route_server_vpc_association:
    example:
      route_server_id: ${aws_vpc_route_server.example.route_server_id}
      vpc_id: ${aws_vpc.example.id}
```
