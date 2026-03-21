# Resource: aws_vpn_gateway_attachment

Provides a Virtual Private Gateway attachment resource, allowing for an existing
hardware VPN gateway to be attached and/or detached from a VPC.

## Basic Example

```yaml
resource:
  aws_vpc:
    network:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpn_gateway:
    vpn:
      tags:
        Name: example-vpn-gateway

resource:
  aws_vpn_gateway_attachment:
    vpn_attachment:
      vpc_id: ${aws_vpc.network.id}
      vpn_gateway_id: ${aws_vpn_gateway.vpn.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_id` - (Required) The ID of the VPC.
* `vpn_gateway_id` - (Required) The ID of the Virtual Private Gateway.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `vpc_id` - The ID of the VPC that Virtual Private Gateway is attached to.
* `vpn_gateway_id` - The ID of the Virtual Private Gateway.
