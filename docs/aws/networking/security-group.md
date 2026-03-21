# Security Group

Manage Security Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_security_group:
    allow_tls:
      name: allow_tls
      description: Allow TLS inbound traffic and all outbound traffic
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: allow_tls

resource:
  aws_vpc_security_group_ingress_rule:
    allow_tls_ipv4:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv4: ${aws_vpc.main.cidr_block}
      from_port: 443
      ip_protocol: tcp
      to_port: 443

resource:
  aws_vpc_security_group_ingress_rule:
    allow_tls_ipv6:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv6: ${aws_vpc.main.ipv6_cidr_block}
      from_port: 443
      ip_protocol: tcp
      to_port: 443

resource:
  aws_vpc_security_group_egress_rule:
    allow_all_traffic_ipv4:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1" # semantically equivalent to all ports

resource:
  aws_vpc_security_group_egress_rule:
    allow_all_traffic_ipv6:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv6: "::/0"
      ip_protocol: "-1" # semantically equivalent to all ports
```

## Usage With Prefix List IDs

```yaml
resource:
  aws_security_group:
    example:
      egress:
        from_port: 0
        to_port: 0
        protocol: -1
        prefix_list_ids: 
          - ${aws_vpc_endpoint.my_endpoint.prefix_list_id}

resource:
  aws_vpc_endpoint:
    my_endpoint:
```

## Removing All Ingress and Egress Rules

```yaml
resource:
  aws_security_group:
    example:
      name: sg
      vpc_id: ${aws_vpc.example.id}
      ingress: []
      egress: []
```

## Recreating a Security Group

```yaml
resource:
  aws_security_group:
    example:
      name: changeable-name
      lifecycle:
        create_before_destroy: true
```
