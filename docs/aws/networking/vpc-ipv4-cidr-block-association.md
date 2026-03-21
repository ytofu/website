# VPC IPV4 CIDR Block Association

Manage VPC IPV4 CIDR Block Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpc_ipv4_cidr_block_association:
    secondary_cidr:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 172.20.0.0/16
```
