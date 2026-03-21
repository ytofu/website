# Resource: aws_ec2_transit_gateway_route_table

Manages an EC2 Transit Gateway Route Table.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_route_table:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `transit_gateway_id` - (Required) Identifier of EC2 Transit Gateway.
* `tags` - (Optional) Key-value tags for the EC2 Transit Gateway Route Table. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - EC2 Transit Gateway Route Table Amazon Resource Name (ARN).
* `default_association_route_table` - Boolean whether this is the default association route table for the EC2 Transit Gateway.
* `default_propagation_route_table` - Boolean whether this is the default propagation route table for the EC2 Transit Gateway.
* `id` - EC2 Transit Gateway Route Table identifier
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_ec2_transit_gateway_route_table.example tgw-rtb-12345678
```
