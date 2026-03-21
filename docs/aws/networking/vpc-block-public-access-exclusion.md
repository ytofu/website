# VPC Block Public Access Exclusion

Manage VPC Block Public Access Exclusion resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    test:
      cidr_block: 10.1.0.0/16

resource:
  aws_vpc_block_public_access_exclusion:
    test:
      vpc_id: ${aws_vpc.test.id}
      internet_gateway_exclusion_mode: allow-bidirectional
```

## Usage with subnet id

```yaml
resource:
  aws_vpc:
    test:
      cidr_block: 10.1.0.0/16

resource:
  aws_subnet:
    test:
      cidr_block: 10.1.1.0/24
      vpc_id: ${aws_vpc.test.id}

resource:
  aws_vpc_block_public_access_exclusion:
    test:
      subnet_id: ${aws_subnet.test.id}
      internet_gateway_exclusion_mode: allow-egress
```
