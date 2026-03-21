# VPC Route Server Endpoint

Manage VPC Route Server Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_route_server_endpoint:
    test:
      route_server_id: ${aws_vpc_route_server.example.route_server_id}
      subnet_id: ${aws_subnet.main.id}
      tags:
        Name: Endpoint A
```
