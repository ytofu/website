# Resource: aws_synthetics_group

Provides a Synthetics Group resource.

## Basic Example

```yaml
resource:
  aws_synthetics_group:
    example:
      name: example
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the group.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Group.
* `group_id` - ID of the Group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_synthetics_group.example example
```
