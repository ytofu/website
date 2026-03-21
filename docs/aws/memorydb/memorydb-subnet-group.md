# Memorydb Subnet Group

Manage Memorydb Subnet Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.0.0/24
      availability_zone: us-west-2a

resource:
  aws_memorydb_subnet_group:
    example:
      name: my-subnet-group
      subnet_ids: 
        - ${aws_subnet.example.id}
```
