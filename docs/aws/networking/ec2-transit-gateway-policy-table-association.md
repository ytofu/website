# Resource: aws_ec2_transit_gateway_policy_table_association

Manages an EC2 Transit Gateway Policy Table association.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_policy_table_association:
    example:
      transit_gateway_attachment_id: ${aws_networkmanager_transit_gateway_peering.example.transit_gateway_peering_attachment_id}
      transit_gateway_policy_table_id: ${aws_ec2_transit_gateway_policy_table.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `transit_gateway_attachment_id` - (Required) Identifier of EC2 Transit Gateway Attachment.
* `transit_gateway_policy_table_id` - (Required) Identifier of EC2 Transit Gateway Policy Table.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - EC2 Transit Gateway Policy Table identifier combined with EC2 Transit Gateway Attachment identifier
* `resource_id` - Identifier of the resource
* `resource_type` - Type of the resource

## Import

```bash
ytofu import aws_ec2_transit_gateway_policy_table_association.example tgw-rtb-12345678_tgw-attach-87654321
```
