# VPC IPV6 CIDR Block Association

Manage VPC IPV6 CIDR Block Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    test:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpc_ipv6_cidr_block_association:
    test:
      ipv6_ipam_pool_id: ${aws_vpc_ipam_pool.test.id}
      vpc_id: ${aws_vpc.test.id}
```
