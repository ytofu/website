# Resource: aws_ec2_transit_gateway_metering_policy

Manages an EC2 Transit Gateway Metering Policy for Flexible Cost Allocation (FCA). A metering policy defines how traffic is metered for cost allocation purposes on a Transit Gateway.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway:
    example:
      tags:
        Name: example

  aws_ec2_transit_gateway_metering_policy:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      tags:
        Name: example```

## With Middlebox Attachments

```yaml
resource:
  aws_ec2_transit_gateway_metering_policy:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      middlebox_attachment_ids: 
        - ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      tags:
        Name: example
```

## Argument Reference

The following arguments are required:

* `transit_gateway_id` - (Required, Forces new resource) EC2 Transit Gateway identifier.

The following arguments are optional:

* `middlebox_attachment_ids` - (Optional) Set of Transit Gateway attachment IDs to designate as middlebox attachments for this metering policy.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value tags for the EC2 Transit Gateway Metering Policy. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - EC2 Transit Gateway Metering Policy ARN.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `transit_gateway_metering_policy_id` - EC2 Transit Gateway Metering Policy identifier.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `update` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_ec2_transit_gateway_metering_policy.example tgw-mp-12345678
```
