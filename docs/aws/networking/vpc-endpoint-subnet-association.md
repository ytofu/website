# VPC Endpoint Subnet Association

Manage VPC Endpoint Subnet Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_subnet_association:
    sn_ec2:
      vpc_endpoint_id: ${aws_vpc_endpoint.ec2.id}
      subnet_id: ${aws_subnet.sn.id}
```
