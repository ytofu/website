# Resource: aws_servicecatalog_portfolio

Provides a resource to create a Service Catalog Portfolio.

## Basic Example

```yaml
resource:
  aws_servicecatalog_portfolio:
    portfolio:
      name: My App Portfolio
      description: List of my organizations apps
      provider_name: Brett
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the portfolio.
* `description` - (Required) Description of the portfolio
* `provider_name` - (Required) Name of the person or organization who owns the portfolio.
* `tags` - (Optional) Tags to apply to the connection. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the Service Catalog Portfolio.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `30m`)
- `read` - (Default `10m`)
- `update` - (Default `30m`)
- `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_servicecatalog_portfolio.testfolio port-12344321
```
