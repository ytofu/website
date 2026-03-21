# NAT Gateway

Manage NAT Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_nat_gateway:
    example:
      allocation_id: ${aws_eip.example.id}
      subnet_id: ${aws_subnet.example.id}
      tags:
        Name: gw NAT
      depends_on: 
        - ${aws_internet_gateway.example}
```

## Public NAT with Secondary Private IP Addresses

```yaml
resource:
  aws_nat_gateway:
    example:
      allocation_id: ${aws_eip.example.id}
      subnet_id: ${aws_subnet.example.id}
      secondary_allocation_ids: 
        - ${aws_eip.secondary.id}
      secondary_private_ip_addresses: 
        - 10.0.1.5
```

## Private NAT

```yaml
resource:
  aws_nat_gateway:
    example:
      connectivity_type: private
      subnet_id: ${aws_subnet.example.id}
```

## Private NAT with Secondary Private IP Addresses

```yaml
resource:
  aws_nat_gateway:
    example:
      connectivity_type: private
      subnet_id: ${aws_subnet.example.id}
      secondary_private_ip_address_count: 7
```

## Regional NAT Gateway with auto mode

```yaml
data:
  aws_availability_zones:
    available:

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_internet_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_nat_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}
      availability_mode: regional
```

## Regional NAT Gateway with manual mode

```yaml
data:
  aws_availability_zones:
    available:

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_internet_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_eip:
    example:
      domain: vpc

resource:
  aws_nat_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}
      availability_mode: regional
      availability_zone_address:
        allocation_ids: 
          - ${aws_eip.example[0].id}
        availability_zone: ${data.aws_availability_zones.available.names[0]}
      availability_zone_address:
        allocation_ids: 
          - ${aws_eip.example[1].id}
          - ${aws_eip.example[2].id}
        availability_zone: ${data.aws_availability_zones.available.names[1]}
```
