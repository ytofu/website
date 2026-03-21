# Default Security Group

Manage Default Security Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

resource:
  aws_default_security_group:
    default:
      vpc_id: ${aws_vpc.mainvpc.id}
      ingress:
        protocol: -1
        self: true
        from_port: 0
        to_port: 0
      egress:
        from_port: 0
        to_port: 0
        protocol: -1
        cidr_blocks: 
          - 0.0.0.0/0
```

## Example Config To Deny All Egress Traffic, Allowing Ingress

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

resource:
  aws_default_security_group:
    default:
      vpc_id: ${aws_vpc.mainvpc.id}
      ingress:
        protocol: -1
        self: true
        from_port: 0
        to_port: 0
```
