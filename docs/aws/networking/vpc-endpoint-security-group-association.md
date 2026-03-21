# Resource: aws_vpc_endpoint_security_group_association

Provides a resource to create an association between a VPC endpoint and a security group.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_security_group_association:
    sg_ec2:
      vpc_endpoint_id: ${aws_vpc_endpoint.ec2.id}
      security_group_id: ${aws_security_group.sg.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `security_group_id` - (Required) The ID of the security group to be associated with the VPC endpoint.
* `vpc_endpoint_id` - (Required) The ID of the VPC endpoint with which the security group will be associated.
* `replace_default_association` - (Optional) Whether this association should replace the association with the VPC's default security group that is created when no security groups are specified during VPC endpoint creation. At most 1 association per-VPC endpoint should be configured with `replace_default_association = true`. `false` should be used when importing resources.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the association.

## Import

```bash
ytofu import aws_vpc_endpoint_security_group_association.example vpce-aaaaaaaa/sg-bbbbbbbbbbbbbbbbb
```
