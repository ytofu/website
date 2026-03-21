# Resource: aws_servicecatalog_tag_option

Manages a Service Catalog Tag Option.

## Basic Example

```yaml
resource:
  aws_servicecatalog_tag_option:
    example:
      key: nyckel
      value: värde
```

## Argument Reference

The following arguments are required:

* `key` - (Required) Tag option key.
* `value` - (Required) Tag option value.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `active` - (Optional) Whether tag option is active. Default is `true`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier (e.g., `tag-pjtvagohlyo3m`).
* `owner_id` - AWS account ID of the owner account that created the tag option.

## Timeouts

Configuration options:

- `create` - (Default `3m`)
- `read` - (Default `10m`)
- `update` - (Default `3m`)
- `delete` - (Default `3m`)

## Import

```bash
ytofu import aws_servicecatalog_tag_option.example tag-pjtvagohlyo3m
```
