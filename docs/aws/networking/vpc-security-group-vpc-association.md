# Resource: aws_vpc_security_group_vpc_association

ytofu resource for managing Security Group VPC Associations.

## Basic Example

```yaml
resource:
  aws_vpc_security_group_vpc_association:
    example:
      security_group_id: sg-05f1f54ab49bb39a3
      vpc_id: vpc-01df9d105095412ba
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `security_group_id` - (Required) The ID of the security group.
* `vpc_id` - (Required) The ID of the VPC to make the association with.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `state` - State of the VPC association. See the [AWS documentation](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_SecurityGroupVpcAssociation.html) for possible values.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_vpc_security_group_vpc_association.example sg-12345,vpc-67890
```
