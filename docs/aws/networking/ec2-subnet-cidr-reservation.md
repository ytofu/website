# EC2 Subnet CIDR Reservation

Manage EC2 Subnet CIDR Reservation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_subnet_cidr_reservation:
    example:
      cidr_block: 10.0.0.16/28
      reservation_type: prefix
      subnet_id: ${aws_subnet.example.id}
```
