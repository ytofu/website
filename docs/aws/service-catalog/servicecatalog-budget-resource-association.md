# Resource: aws_servicecatalog_budget_resource_association

Manages a Service Catalog Budget Resource Association.

## Basic Example

```yaml
resource:
  aws_servicecatalog_budget_resource_association:
    example:
      budget_name: budget-pjtvyakdlyo3m
      resource_id: prod-dnigbtea24ste
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `budget_name` - (Required) Budget name.
* `resource_id` - (Required) Resource identifier.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier of the association.

## Timeouts

Configuration options:

- `create` - (Default `3m`)
- `read` - (Default `10m`)
- `delete` - (Default `3m`)

## Import

```bash
ytofu import aws_servicecatalog_budget_resource_association.example budget-pjtvyakdlyo3m:prod-dnigbtea24ste
```
