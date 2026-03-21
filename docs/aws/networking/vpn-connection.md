# VPN Connection

Manage VPN Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway:
    example:

resource:
  aws_customer_gateway:
    example:
      bgp_asn: 65000
      ip_address: 172.0.0.1
      type: ipsec.1

resource:
  aws_vpn_connection:
    example:
      customer_gateway_id: ${aws_customer_gateway.example.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      type: ${aws_customer_gateway.example.type}
```

## Virtual Private Gateway

```yaml
resource:
  aws_vpc:
    vpc:
      cidr_block: 10.0.0.0/16

resource:
  aws_vpn_gateway:
    vpn_gateway:
      vpc_id: ${aws_vpc.vpc.id}

resource:
  aws_customer_gateway:
    customer_gateway:
      bgp_asn: 65000
      ip_address: 172.0.0.1
      type: ipsec.1

resource:
  aws_vpn_connection:
    main:
      vpn_gateway_id: ${aws_vpn_gateway.vpn_gateway.id}
      customer_gateway_id: ${aws_customer_gateway.customer_gateway.id}
      type: ipsec.1
      static_routes_only: true
```

## AWS Site to Site Private VPN

```yaml
resource:
  aws_dx_gateway:
    example:
      name: terraform_ipsec_vpn_example
      amazon_side_asn: 64512

resource:
  aws_ec2_transit_gateway:
    example:
      amazon_side_asn: 64513
      description: terraform_ipsec_vpn_example
      transit_gateway_cidr_blocks:
        - 10.0.0.0/24

resource:
  aws_customer_gateway:
    example:
      bgp_asn: 64514
      ip_address: 10.0.0.1
      type: ipsec.1
      tags:
        Name: terraform_ipsec_vpn_example

resource:
  aws_dx_gateway_association:
    example:
      dx_gateway_id: ${aws_dx_gateway.example.id}
      associated_gateway_id: ${aws_ec2_transit_gateway.example.id}
      allowed_prefixes:
        - 10.0.0.0/8

data:
  aws_ec2_transit_gateway_dx_gateway_attachment:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      dx_gateway_id: ${aws_dx_gateway.example.id}
      depends_on:
        - ${aws_dx_gateway_association.example}

resource:
  aws_vpn_connection:
    example:
      customer_gateway_id: ${aws_customer_gateway.example.id}
      outside_ip_address_type: PrivateIpv4
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      transport_transit_gateway_attachment_id: ${data.aws_ec2_transit_gateway_dx_gateway_attachment.example.id}
      type: ipsec.1
      tags:
        Name: terraform_ipsec_vpn_example
```
