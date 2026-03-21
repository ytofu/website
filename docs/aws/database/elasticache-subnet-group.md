# Resource: aws_elasticache_subnet_group

Provides an ElastiCache Subnet Group resource.

## Basic Example

```yaml
resource:
  aws_vpc:
    foo:
      cidr_block: 10.0.0.0/16
      tags:
        Name: tf-test

resource:
  aws_subnet:
    foo:
      vpc_id: ${aws_vpc.foo.id}
      cidr_block: 10.0.0.0/24
      availability_zone: us-west-2a
      tags:
        Name: tf-test

resource:
  aws_elasticache_subnet_group:
    bar:
      name: tf-test-cache-subnet
      subnet_ids: 
        - ${aws_subnet.foo.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name for the cache subnet group. ElastiCache converts this name to lowercase.
* `description` - (Optional) Description for the cache subnet group. Defaults to "Managed by ytofu".
* `subnet_ids` - (Required) List of VPC Subnet IDs for the cache subnet group
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `vpc_id` - The Amazon Virtual Private Cloud identifier (VPC ID) of the cache subnet group.

## Import

```bash
ytofu import aws_elasticache_subnet_group.bar tf-test-cache-subnet
```
