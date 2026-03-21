# Resource: aws_nat_gateway_eip_association

ytofu resource for managing an AWS VPC NAT Gateway EIP Association.

## Basic Example

```yaml
resource:
  aws_nat_gateway_eip_association:
    example:
      allocation_id: ${aws_eip.example.id}
      nat_gateway_id: ${aws_nat_gateway.example.id}
```

## Argument Reference

The following arguments are required:

* `allocation_id` - (Required) The ID of the Elastic IP Allocation to associate with the NAT Gateway.
* `nat_gateway_id` - (Required) The ID of the NAT Gateway to associate the Elastic IP Allocation to.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_nat_gateway_eip_association.example nat-1234567890abcdef1,eipalloc-1234567890abcdef1
```
