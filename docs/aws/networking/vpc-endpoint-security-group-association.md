# VPC Endpoint Security Group Association

Manage VPC Endpoint Security Group Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_security_group_association:
    sg_ec2:
      vpc_endpoint_id: ${aws_vpc_endpoint.ec2.id}
      security_group_id: ${aws_security_group.sg.id}
```
