# Workspacesweb Network Settings Association

Manage Workspacesweb Network Settings Association resources using ytofu YAML.

## Basic Example

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
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16
      tags:
        Name: example

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.1.0/24
      availability_zone: ${data.aws_availability_zones.available.names[count.index]}
      tags:
        Name: example

resource:
  aws_security_group:
    example:
      vpc_id: ${aws_vpc.example.id}
      name: "example-${count.index}"
      tags:
        Name: example

resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

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

resource:
  aws_workspacesweb_network_settings_association:
    example:
      network_settings_arn: ${aws_workspacesweb_network_settings.example.network_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
```
