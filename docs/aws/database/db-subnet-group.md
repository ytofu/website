# Resource: aws_db_subnet_group

Provides an RDS DB subnet group resource.

## Basic Example

```yaml
resource:
  aws_db_subnet_group:
    default:
      name: main
      subnet_ids: 
        - ${aws_subnet.frontend.id}
        - ${aws_subnet.backend.id}
      tags:
        Name: My DB subnet group
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) The name of the DB subnet group. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `description` - (Optional) The description of the DB subnet group. Defaults to "Managed by ytofu".
* `subnet_ids` - (Required) A list of VPC subnet IDs.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The db subnet group name.
* `arn` - The ARN of the db subnet group.
* `supported_network_types` - The network type of the db subnet group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `vpc_id` - Provides the VPC ID of the DB subnet group.

## Import

```bash
ytofu import aws_db_subnet_group.default production-subnet-group
```
