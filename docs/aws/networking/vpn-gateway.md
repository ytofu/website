# Resource: aws_vpn_gateway

Provides a resource to create a VPC VPN Gateway.

## Basic Example

```yaml
resource:
  aws_vpn_gateway:
    vpn_gw:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_id` - (Optional) The VPC ID to create in.
* `availability_zone` - (Optional) The Availability Zone for the virtual private gateway.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `amazon_side_asn` - (Optional) The Autonomous System Number (ASN) for the Amazon side of the gateway. If you don't specify an ASN, the virtual private gateway is created with the default ASN.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the VPN Gateway.
* `id` - The ID of the VPN Gateway.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_vpn_gateway.testvpngateway vgw-9a4cacf3
```
