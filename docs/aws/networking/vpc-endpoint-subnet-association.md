# Resource: aws_vpc_endpoint_subnet_association

Provides a resource to create an association between a VPC endpoint and a subnet.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_subnet_association:
    sn_ec2:
      vpc_endpoint_id: ${aws_vpc_endpoint.ec2.id}
      subnet_id: ${aws_subnet.sn.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_endpoint_id` - (Required) The ID of the VPC endpoint with which the subnet will be associated.
* `subnet_id` - (Required) The ID of the subnet to be associated with the VPC endpoint.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the association.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_vpc_endpoint_subnet_association.example vpce-aaaaaaaa/subnet-bbbbbbbbbbbbbbbbb
```
