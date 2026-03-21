# Resource: aws_ec2_transit_gateway_route_table_propagation

Manages an EC2 Transit Gateway Route Table propagation.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_route_table_propagation:
    example:
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway_route_table.example.id}
```

## Direct Connect Gateway Propagation

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
  aws_ec2_transit_gateway_route_table_propagation:
    example:
      transit_gateway_attachment_id: ${aws_dx_gateway_association.example.transit_gateway_attachment_id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway_route_table.example.id}
```

## VPC Attachment Propagation

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
  aws_ec2_transit_gateway_route_table_propagation:
    example:
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway_route_table.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `transit_gateway_attachment_id` - (Required) Identifier of EC2 Transit Gateway Attachment.
* `transit_gateway_route_table_id` - (Required) Identifier of EC2 Transit Gateway Route Table.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - EC2 Transit Gateway Route Table identifier combined with EC2 Transit Gateway Attachment identifier
* `resource_id` - Identifier of the resource
* `resource_type` - Type of the resource

## Import

```bash
ytofu import aws_ec2_transit_gateway_route_table_propagation.example tgw-rtb-12345678_tgw-attach-87654321
```
