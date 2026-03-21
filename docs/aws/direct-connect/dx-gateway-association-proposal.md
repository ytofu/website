# Resource: aws_dx_gateway_association_proposal

Manages a Direct Connect Gateway Association Proposal, typically for enabling cross-account associations. For single account associations, see the `aws_dx_gateway_association` resource.

## Basic Example

```yaml
resource:
  aws_dx_gateway_association_proposal:
    example:
      dx_gateway_id: ${aws_dx_gateway.example.id}
      dx_gateway_owner_account_id: ${aws_dx_gateway.example.owner_account_id}
      associated_gateway_id: ${aws_vpn_gateway.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `associated_gateway_id` - (Required) The ID of the VGW or transit gateway with which to associate the Direct Connect gateway.
* `dx_gateway_id` - (Required) Direct Connect Gateway identifier.
* `dx_gateway_owner_account_id` - (Required) AWS Account identifier of the Direct Connect Gateway's owner.
* `allowed_prefixes` - (Optional) VPC prefixes (CIDRs) to advertise to the Direct Connect gateway. Defaults to the CIDR block of the VPC associated with the Virtual Gateway. To enable drift detection, must be configured.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Direct Connect Gateway Association Proposal identifier.
* `associated_gateway_owner_account_id` - The ID of the AWS account that owns the VGW or transit gateway with which to associate the Direct Connect gateway.
* `associated_gateway_type` - The type of the associated gateway, `transitGateway` or `virtualPrivateGateway`.
