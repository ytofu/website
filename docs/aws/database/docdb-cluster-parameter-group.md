# Resource: aws_docdb_cluster_parameter_group

Manages a DocumentDB Cluster Parameter Group

## Basic Example

```yaml
resource:
  aws_docdb_cluster_parameter_group:
    example:
      family: docdb3.6
      name: example
      description: docdb cluster parameter group
      parameter:
        name: tls
        value: enabled
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) The name of the DocumentDB cluster parameter group. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `family` - (Required, Forces new resource) The family of the DocumentDB cluster parameter group.
* `description` - (Optional, Forces new resource) The description of the DocumentDB cluster parameter group. Defaults to "Managed by ytofu".
* `parameter` - (Optional) A list of DocumentDB parameters to apply. Setting parameters to system default values may show a difference on imported resources.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

Parameter blocks support the following:

* `name` - (Required) The name of the DocumentDB parameter.
* `value` - (Required) The value of the DocumentDB parameter.
* `apply_method` - (Optional) Valid values are `immediate` and `pending-reboot`. Defaults to `pending-reboot`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The DocumentDB cluster parameter group name.
* `arn` - The ARN of the DocumentDB cluster parameter group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_docdb_cluster_parameter_group.cluster_pg production-pg-1
```
