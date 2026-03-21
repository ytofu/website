# Resource: aws_vpn_concentrator

Provides a resource to create a VPN Concentrator that aggregates multiple VPN connections to a transit gateway.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway:
    example:
      description: example
      tags:
        Name: example

resource:
  aws_vpn_concentrator:
    example:
      type: ipsec.1
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      tags:
        Name: example
```

## Argument Reference

The following arguments are required:

* `type` - (Required) Type of VPN concentrator. Valid value: `ipsec.1`.
* `transit_gateway_id` - (Required) ID of the transit gateway to attach the VPN concentrator to.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `vpn_concentrator_id` - ID of the VPN Concentrator.
* `transit_gateway_attachment_id` - ID of the transit gateway attachment created for the VPN concentrator.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_vpn_concentrator.example vcn-12345678
```
