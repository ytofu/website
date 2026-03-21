# EC2 Transit Gateway VPC Attachment Accepter

Manage EC2 Transit Gateway VPC Attachment Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_vpc_attachment_accepter:
    example:
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      tags:
        Name: Example cross-account attachment
```
