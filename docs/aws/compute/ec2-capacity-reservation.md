# EC2 Capacity Reservation

Manage EC2 Capacity Reservation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_capacity_reservation:
    default:
      instance_type: t2.micro
      instance_platform: Linux/UNIX
      availability_zone: eu-west-1a
      instance_count: 1
```
