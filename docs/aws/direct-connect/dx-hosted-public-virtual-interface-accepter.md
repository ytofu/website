# Resource: aws_dx_hosted_public_virtual_interface_accepter

Provides a resource to manage the accepter's side of a Direct Connect hosted public virtual interface.
This resource accepts ownership of a public virtual interface created by another AWS account.

## Basic Example

```yaml
data:
  aws_caller_identity:
    accepter:

resource:
  aws_dx_hosted_public_virtual_interface:
    creator:
      connection_id: dxcon-zzzzzzzz
      owner_account_id: ${data.aws_caller_identity.accepter.account_id}
      name: vif-foo
      vlan: 4094
      address_family: ipv4
      bgp_asn: 65352
      customer_address: 175.45.176.1/30
      amazon_address: 175.45.176.2/30
      route_filter_prefixes:
        - 210.52.109.0/24
        - 175.45.176.0/22

resource:
  aws_dx_hosted_public_virtual_interface_accepter:
    accepter:
      virtual_interface_id: ${aws_dx_hosted_public_virtual_interface.creator.id}
      tags:
        Side: Accepter
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `virtual_interface_id` - (Required) The ID of the Direct Connect virtual interface to accept.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### Removing `aws_dx_hosted_public_virtual_interface_accepter` from your configuration

AWS allows a Direct Connect hosted public virtual interface to be deleted from either the allocator's or accepter's side.
However, ytofu only allows the Direct Connect hosted public virtual interface to be deleted from the allocator's side
by removing the corresponding `aws_dx_hosted_public_virtual_interface` resource from your configuration.
Removing a `aws_dx_hosted_public_virtual_interface_accepter` resource from your configuration will remove it
from your statefile and management, **but will not delete the Direct Connect virtual interface.**

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
ytofu import aws_dx_hosted_public_virtual_interface_accepter.test dxvif-33cc44dd
```
