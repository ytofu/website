# EC2 Transit Gateway Metering Policy

Manage EC2 Transit Gateway Metering Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway:
    example:
      tags:
        Name: example

resource:
  aws_ec2_transit_gateway_metering_policy:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      tags:
        Name: example
```

## With Middlebox Attachments

```yaml
resource:
  aws_ec2_transit_gateway_metering_policy:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      middlebox_attachment_ids: 
        - ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      tags:
        Name: example
```
