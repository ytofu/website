# Resource: aws_servicecatalog_tag_option_resource_association

Manages a Service Catalog Tag Option Resource Association.

## Basic Example

```yaml
resource:
  aws_servicecatalog_tag_option_resource_association:
    example:
      resource_id: prod-dnigbtea24ste
      tag_option_id: tag-pjtvyakdlyo3m
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_id` - (Required) Resource identifier.
* `tag_option_id` - (Required) Tag Option identifier.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier of the association.
* `resource_arn` - ARN of the resource.
* `resource_created_time` - Creation time of the resource.
* `resource_description` - Description of the resource.
* `resource_name` - Description of the resource.

## Timeouts

Configuration options:

- `create` - (Default `3m`)
- `read` - (Default `10m`)
- `delete` - (Default `3m`)

## Import

```bash
ytofu import aws_servicecatalog_tag_option_resource_association.example tag-pjtvyakdlyo3m:prod-dnigbtea24ste
```
