# EC2 Capacity Block Reservation

Manage EC2 Capacity Block Reservation resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_ec2_capacity_block_offering:
    test:
      capacity_duration_hours: 24
      end_date_range: "2024-05-30T15:04:05Z"
      instance_count: 1
      instance_type: p4d.24xlarge
      start_date_range: "2024-04-28T15:04:05Z"

resource:
  aws_ec2_capacity_block_reservation:
    example:
      capacity_block_offering_id: ${data.aws_ec2_capacity_block_offering.test.capacity_block_offering_id}
      instance_platform: Linux/UNIX
      tags: 
```
