# Resource: aws_dx_hosted_transit_virtual_interface_accepter

Provides a resource to manage the accepter's side of a Direct Connect hosted transit virtual interface.
This resource accepts ownership of a transit virtual interface created by another AWS account.

## Basic Example

```yaml
data:
  aws_caller_identity:
    accepter:

resource:
  aws_dx_hosted_transit_virtual_interface:
    creator:
      connection_id: dxcon-zzzzzzzz
      owner_account_id: ${data.aws_caller_identity.accepter.account_id}
      name: tf-transit-vif-example
      vlan: 4094
      address_family: ipv4
      bgp_asn: 65352
      depends_on: 
        - ${aws_dx_gateway.example}

resource:
  aws_dx_gateway:
    example:
      name: tf-dxg-example
      amazon_side_asn: 64512

resource:
  aws_dx_hosted_transit_virtual_interface_accepter:
    accepter:
      virtual_interface_id: ${aws_dx_hosted_transit_virtual_interface.creator.id}
      dx_gateway_id: ${aws_dx_gateway.example.id}
      tags:
        Side: Accepter
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `dx_gateway_id` - (Required) The ID of the [Direct Connect gateway](dx_gateway.html) to which to connect the virtual interface.
* `virtual_interface_id` - (Required) The ID of the Direct Connect virtual interface to accept.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the virtual interface.
* `arn` - The ARN of the virtual interface.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_dx_hosted_transit_virtual_interface_accepter.test dxvif-33cc44dd
```
