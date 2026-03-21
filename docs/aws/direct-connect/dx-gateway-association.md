# Resource: aws_dx_gateway_association

Associates a Direct Connect Gateway with a VGW or transit gateway.

## Basic Example

```yaml
resource:
  aws_dx_gateway:
    example:
      name: example
      amazon_side_asn: 64512

  aws_vpc:
    example:
      cidr_block: 10.255.255.0/28

  aws_vpn_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}

  aws_dx_gateway_association:
    example:
      dx_gateway_id: ${aws_dx_gateway.example.id}
      associated_gateway_id: ${aws_vpn_gateway.example.id}```

## Transit Gateway Association

```yaml
resource:
  aws_dx_gateway:
    example:
      name: example
      amazon_side_asn: 64512

  aws_ec2_transit_gateway:
    example:

  aws_dx_gateway_association:
    example:
      dx_gateway_id: ${aws_dx_gateway.example.id}
      associated_gateway_id: ${aws_ec2_transit_gateway.example.id}
      allowed_prefixes:
        - 10.255.255.0/30
        - 10.255.255.8/30```

## Allowed Prefixes

```yaml
resource:
  aws_dx_gateway:
    example:
      name: example
      amazon_side_asn: 64512

  aws_vpc:
    example:
      cidr_block: 10.255.255.0/28

  aws_vpn_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}

  aws_dx_gateway_association:
    example:
      dx_gateway_id: ${aws_dx_gateway.example.id}
      associated_gateway_id: ${aws_vpn_gateway.example.id}
      allowed_prefixes:
        - 210.52.109.0/24
        - 175.45.176.0/22```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `dx_gateway_id` - (Required) The ID of the Direct Connect gateway.
* `associated_gateway_id` - (Optional) The ID of the VGW or transit gateway with which to associate the Direct Connect gateway.
Used for single account Direct Connect gateway associations.
* `associated_gateway_owner_account_id` - (Optional) The ID of the AWS account that owns the VGW or transit gateway with which to associate the Direct Connect gateway.
Used for cross-account Direct Connect gateway associations.
* `proposal_id` - (Optional) The ID of the Direct Connect gateway association proposal.
Used for cross-account Direct Connect gateway associations.
* `allowed_prefixes` - (Optional) VPC prefixes (CIDRs) to advertise to the Direct Connect gateway. Defaults to the CIDR block of the VPC associated with the Virtual Gateway. To enable drift detection, must be configured.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `associated_gateway_type` - The type of the associated gateway, `transitGateway` or `virtualPrivateGateway`.
* `dx_gateway_association_id` - The ID of the Direct Connect gateway association.
* `dx_gateway_owner_account_id` - The ID of the AWS account that owns the Direct Connect gateway.
* `transit_gateway_attachment_id` - The ID of the Transit Gateway Attachment when the type is `transitGateway`.

## Timeouts

Configuration options:

- `create` - (Default `30m`)
- `update` - (Default `30m`)
- `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_dx_gateway_association.example 345508c3-7215-4aef-9832-07c125d5bd0f/vgw-98765432
```
