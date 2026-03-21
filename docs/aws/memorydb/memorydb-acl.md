# Resource: aws_memorydb_acl

Provides a MemoryDB ACL.

## Basic Example

```yaml
resource:
  aws_memorydb_acl:
    example:
      name: my-acl
      user_names: 
        - my-user-1
        - my-user-2
```

## Argument Reference

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) Name of the ACL. If omitted, ytofu will assign a random, unique name. Conflicts with `name_prefix`.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `user_names` - (Optional) Set of MemoryDB user names to be included in this ACL.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Same as `name`.
* `arn` - The ARN of the ACL.
* `minimum_engine_version` - The minimum engine version supported by the ACL.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_memorydb_acl.example my-acl
```
