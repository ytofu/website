# Resource: aws_dax_subnet_group

Provides a DAX Subnet Group resource.

## Basic Example

```yaml
resource:
  aws_dax_subnet_group:
    example:
      name: example
      subnet_ids: 
        - ${aws_subnet.example1.id}
        - ${aws_subnet.example2.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the subnet group.
* `description` - (Optional) A description of the subnet group.
* `subnet_ids` - (Required) A list of VPC subnet IDs for the subnet group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the subnet group.
* `vpc_id` - VPC ID of the subnet group.

## Import

```bash
ytofu import aws_dax_subnet_group.example my_dax_sg
```
