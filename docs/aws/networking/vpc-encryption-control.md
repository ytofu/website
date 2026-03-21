# VPC Encryption Control

Manage VPC Encryption Control resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_encryption_control:
    example:
      vpc_id: ${aws_vpc.example.id}
      mode: monitor

resource:
  aws_vpc:
    example:
      cidr_block: 10.1.0.0/16
```
