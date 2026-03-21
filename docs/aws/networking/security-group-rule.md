# Security Group Rule

Manage Security Group Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_security_group_rule:
    example:
      type: ingress
      from_port: 0
      to_port: 65535
      protocol: tcp
      cidr_blocks: 
        - ${aws_vpc.example.cidr_block}
      ipv6_cidr_blocks: 
        - ${aws_vpc.example.ipv6_cidr_block}
      security_group_id: sg-123456
```

## Usage With Prefix List IDs

```yaml
resource:
  aws_security_group_rule:
    allow_all:
      type: egress
      to_port: 0
      protocol: -1
      prefix_list_ids: 
        - ${aws_vpc_endpoint.my_endpoint.prefix_list_id}
      from_port: 0
      security_group_id: sg-123456

resource:
  aws_vpc_endpoint:
    my_endpoint:
```
