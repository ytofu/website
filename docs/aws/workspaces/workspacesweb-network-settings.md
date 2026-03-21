# Workspacesweb Network Settings

Manage Workspacesweb Network Settings resources using ytofu YAML.

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
      cidr_block: 10.0.1.0/24
      availability_zone: ${data.aws_availability_zones.available.names[count.index]}

resource:
  aws_security_group:
    example1:
      vpc_id: ${aws_vpc.example.id}
      name: "example-sg-${count.index}$"

resource:
  aws_workspacesweb_network_settings:
    example:
      vpc_id: ${aws_vpc.example.id}
      subnet_ids: 
        - ${aws_subnet.example[0].id}
        - ${aws_subnet.example[1].id}
      security_group_ids: 
        - ${aws_security_group.example[0].id}
        - ${aws_security_group.example[1].id}
```
