# Resource: aws_ec2_transit_gateway_policy_table

Manages an EC2 Transit Gateway Policy Table.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_policy_table:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      tags:
        Name: Example Policy Table
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `transit_gateway_id` - (Required) EC2 Transit Gateway identifier.
* `tags` - (Optional) Key-value tags for the EC2 Transit Gateway Policy Table. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - EC2 Transit Gateway Policy Table Amazon Resource Name (ARN).
* `id` - EC2 Transit Gateway Policy Table identifier.
* `state` - The state of the EC2 Transit Gateway Policy Table.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_ec2_transit_gateway_policy_table.example tgw-rtb-12345678
```
