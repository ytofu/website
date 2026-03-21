# EC2 Secondary Network

Manage EC2 Secondary Network resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_secondary_network:
    example:
      ipv4_cidr_block: 10.0.0.0/16
      network_type: rdma
      tags:
        Name: example-secondary-network
```
