# EC2 Availability Zone Group

Manage EC2 Availability Zone Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_availability_zone_group:
    example:
      group_name: us-west-2-lax-1
      opt_in_status: opted-in
```
