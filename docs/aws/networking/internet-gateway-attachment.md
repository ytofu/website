# Internet Gateway Attachment

Manage Internet Gateway Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_internet_gateway_attachment:
    example:
      internet_gateway_id: ${aws_internet_gateway.example.id}
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_vpc:
    example:
      cidr_block: 10.1.0.0/16

resource:
  aws_internet_gateway:
    example:
```
