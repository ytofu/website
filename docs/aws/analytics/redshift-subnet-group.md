# Resource: aws_redshift_subnet_group

Creates a new Amazon Redshift subnet group. You must provide a list of one or more subnets in your existing Amazon Virtual Private Cloud (Amazon VPC) when creating Amazon Redshift subnet group.

## Basic Example

```yaml
resource:
  aws_vpc:
    foo:
      cidr_block: 10.1.0.0/16

resource:
  aws_subnet:
    foo:
      cidr_block: 10.1.1.0/24
      availability_zone: us-west-2a
      vpc_id: ${aws_vpc.foo.id}
      tags:
        Name: tf-dbsubnet-test-1

resource:
  aws_subnet:
    bar:
      cidr_block: 10.1.2.0/24
      availability_zone: us-west-2b
      vpc_id: ${aws_vpc.foo.id}
      tags:
        Name: tf-dbsubnet-test-2

resource:
  aws_redshift_subnet_group:
    foo:
      name: foo
      subnet_ids: 
        - ${aws_subnet.foo.id}
        - ${aws_subnet.bar.id}
      tags:
        environment: Production
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the Redshift Subnet group.
* `description` - (Optional) The description of the Redshift Subnet group. Defaults to "Managed by ytofu".
* `subnet_ids` - (Required) An array of VPC subnet IDs.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the Redshift Subnet group name
* `id` - The Redshift Subnet group ID.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_redshift_subnet_group.testgroup1 test-cluster-subnet-group
```
