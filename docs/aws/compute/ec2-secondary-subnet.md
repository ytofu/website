# EC2 Secondary Subnet

Manage EC2 Secondary Subnet resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_secondary_network:
    example:
      ipv4_cidr_block: 10.0.0.0/16
      network_type: rdma
      tags:
        Name: example-secondary-network

resource:
  aws_ec2_secondary_subnet:
    example:
      secondary_network_id: ${aws_ec2_secondary_network.example.id}
      ipv4_cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a
      tags:
        Name: example-secondary-subnet
```

## Using Availability Zone ID

```yaml
data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_ec2_secondary_network:
    example:
      ipv4_cidr_block: 10.0.0.0/16
      network_type: rdma
      tags:
        Name: example-secondary-network

resource:
  aws_ec2_secondary_subnet:
    example:
      secondary_network_id: ${aws_ec2_secondary_network.example.id}
      ipv4_cidr_block: 10.0.1.0/24
      availability_zone_id: ${data.aws_availability_zones.available.zone_ids[0]}
      tags:
        Name: example-secondary-subnet
```
