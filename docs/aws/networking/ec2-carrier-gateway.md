# EC2 Carrier Gateway

Manage EC2 Carrier Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_carrier_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}
      tags:
        Name: example-carrier-gateway
```
