# Resource: aws_keyspaces_keyspace

Provides a Keyspaces Keyspace.

## Basic Example

```yaml
resource:
  aws_keyspaces_keyspace:
    example:
      name: my_keyspace
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required, Forces new resource) The name of the keyspace to be created.
* `replication_specification` - (Optional) The replication specification of the keyspace.
    * `region_list` - (Optional) Replication regions. If `replication_strategy` is `MULTI_REGION`, `region_list` requires the current Region and at least one additional AWS Region where the keyspace is going to be replicated in.
    * `replication_strategy` - (Required) Replication strategy. Valid values: `SINGLE_REGION` and `MULTI_REGION`.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the keyspace.
* `arn` - The ARN of the keyspace.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `1m`)
- `delete` - (Default `1m`)

## Import

```bash
ytofu import aws_keyspaces_keyspace.example my_keyspace
```
