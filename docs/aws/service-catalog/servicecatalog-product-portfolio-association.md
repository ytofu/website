# Resource: aws_servicecatalog_product_portfolio_association

Manages a Service Catalog Product Portfolio Association.

## Basic Example

```yaml
resource:
  aws_servicecatalog_product_portfolio_association:
    example:
      portfolio_id: port-68656c6c6f
      product_id: prod-dnigbtea24ste
```

## Argument Reference

The following arguments are required:

* `portfolio_id` - (Required) Portfolio identifier.
* `product_id` - (Required) Product identifier.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `accept_language` - (Optional) Language code. Valid values: `en` (English), `jp` (Japanese), `zh` (Chinese). Default value is `en`.
* `source_portfolio_id` - (Optional) Identifier of the source portfolio.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier of the association.

Configuration options:

- `create` - (Default `3m`)
- `read` - (Default `10m`)
- `delete` - (Default `3m`)

## Import

```bash
ytofu import aws_servicecatalog_product_portfolio_association.example en:port-68656c6c6f:prod-dnigbtea24ste
```
