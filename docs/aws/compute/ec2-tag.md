# Resource: aws_ec2_tag

Manages an individual EC2 resource tag. This resource should only be used in cases where EC2 resources are created outside ytofu (e.g., AMIs), being shared via Resource Access Manager (RAM), or implicitly created by other means (e.g., Transit Gateway VPN Attachments).

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

resource:
  aws_ec2_tag:
    example:
      resource_id: ${aws_vpn_connection.example.transit_gateway_attachment_id}
      key: Name
      value: Hello World
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_id` - (Required) The ID of the EC2 resource to manage the tag for.
* `key` - (Required) The tag name.
* `value` - (Required) The value of the tag.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - EC2 resource identifier and key, separated by a comma (`,`)

## Import

```bash
ytofu import aws_ec2_tag.example tgw-attach-1234567890abcdef,Name
```
