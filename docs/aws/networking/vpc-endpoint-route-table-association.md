# Resource: aws_vpc_endpoint_route_table_association

Manages a VPC Endpoint Route Table Association

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_route_table_association:
    example:
      route_table_id: ${aws_route_table.example.id}
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `route_table_id` - (Required) Identifier of the EC2 Route Table to be associated with the VPC Endpoint.
* `vpc_endpoint_id` - (Required) Identifier of the VPC Endpoint with which the EC2 Route Table will be associated.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A hash of the EC2 Route Table and VPC Endpoint identifiers.

## Import

```bash
ytofu import aws_vpc_endpoint_route_table_association.example vpce-aaaaaaaa/rtb-bbbbbbbb
```
