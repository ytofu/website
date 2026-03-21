# Vpclattice Resource Gateway

Manage Vpclattice Resource Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_resource_gateway:
    example:
      name: Example
      vpc_id: ${aws_vpc.example.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
      tags:
        Environment: Example
```

## Specifying IP address type

```yaml
resource:
  aws_vpclattice_resource_gateway:
    example:
      name: Example
      vpc_id: ${aws_vpc.example.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
      ip_address_type: DUALSTACK
      tags:
        Environment: Example
```

## With security groups

```yaml
resource:
  aws_vpclattice_resource_gateway:
    example:
      name: Example
      vpc_id: ${aws_vpc.example.id}
      security_group_ids: 
        - ${aws_security_group.test.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
```
