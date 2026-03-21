# EC2 Transit Gateway Route Table Association

Manage EC2 Transit Gateway Route Table Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_route_table_association:
    example:
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway_route_table.example.id}
```

## Direct Connect Gateway Association

```yaml
resource:
  aws_dx_gateway:
    example:
      name: example
      amazon_side_asn: 64512

resource:
  aws_ec2_transit_gateway:
    example:
      description: example

resource:
  aws_dx_gateway_association:
    example:
      dx_gateway_id: ${aws_dx_gateway.example.id}
      associated_gateway_id: ${aws_ec2_transit_gateway.example.id}
      allowed_prefixes:
        - 10.0.0.0/16

resource:
  aws_ec2_transit_gateway_route_table:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}

resource:
  aws_ec2_transit_gateway_route_table_association:
    example:
      transit_gateway_attachment_id: ${aws_dx_gateway_association.example.transit_gateway_attachment_id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway_route_table.example.id}
```

## VPC Attachment Association

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.1.0/24

resource:
  aws_ec2_transit_gateway:
    example:
      description: example

resource:
  aws_ec2_transit_gateway_vpc_attachment:
    example:
      subnet_ids: 
        - ${aws_subnet.example.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_ec2_transit_gateway_route_table:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}

resource:
  aws_ec2_transit_gateway_route_table_association:
    example:
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway_route_table.example.id}
```
