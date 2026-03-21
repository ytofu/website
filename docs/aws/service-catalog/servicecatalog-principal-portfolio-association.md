# Resource: aws_servicecatalog_principal_portfolio_association

Manages a Service Catalog Principal Portfolio Association.

## Basic Example

```yaml
resource:
  aws_servicecatalog_principal_portfolio_association:
    example:
      portfolio_id: port-68656c6c6f
      principal_arn: "arn:aws:iam::123456789012:user/Eleanor"
```

## Argument Reference

The following arguments are required:

* `portfolio_id` - (Required) Portfolio identifier.
* `principal_arn` - (Required) Principal ARN.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `accept_language` - (Optional) Language code. Valid values: `en` (English), `jp` (Japanese), `zh` (Chinese). Default value is `en`.
* `principal_type` - (Optional) Principal type. Setting this argument empty (e.g., `principal_type = ""`) will result in an error. Valid values are `IAM` and `IAM_PATTERN`. Default is `IAM`.

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
ytofu import aws_servicecatalog_principal_portfolio_association.example en,arn:aws:iam::123456789012:user/Eleanor,port-68656c6c6f,IAM
```
