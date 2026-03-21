# Resource: aws_servicecatalog_portfolio_share

Manages a Service Catalog Portfolio Share. Shares the specified portfolio with the specified account or organization node. You can share portfolios to an organization, an organizational unit, or a specific account.

## Basic Example

```yaml
resource:
  aws_servicecatalog_portfolio_share:
    example:
      principal_id: 012128675309
      portfolio_id: ${aws_servicecatalog_portfolio.example.id}
      type: ACCOUNT
```

## Argument Reference

The following arguments are required:

* `portfolio_id` - (Required) Portfolio identifier.
* `principal_id` - (Required) Identifier of the principal with whom you will share the portfolio. Valid values AWS account IDs and ARNs of AWS Organizations and organizational units.
* `type` - (Required) Type of portfolio share. Valid values are `ACCOUNT` (an external account), `ORGANIZATION` (a share to every account in an organization), `ORGANIZATIONAL_UNIT`, `ORGANIZATION_MEMBER_ACCOUNT` (a share to an account in an organization).

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `accept_language` - (Optional) Language code. Valid values: `en` (English), `jp` (Japanese), `zh` (Chinese). Default value is `en`.
* `share_principals` - (Optional) Enables or disables Principal sharing when creating the portfolio share. If this flag is not provided, principal sharing is disabled.
* `share_tag_options` - (Optional) Whether to enable sharing of `aws_servicecatalog_tag_option` resources when creating the portfolio share.
* `wait_for_acceptance` - (Optional) Whether to wait (up to the timeout) for the share to be accepted. Organizational shares are automatically accepted.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `accepted` - Whether the shared portfolio is imported by the recipient account. If the recipient is organizational, the share is automatically imported, and the field is always set to true.

## Timeouts

Configuration options:

- `create` - (Default `3m`)
- `read` - (Default `10m`)
- `update` - (Default `3m`)
- `delete` - (Default `3m`)

## Import

```bash
ytofu import aws_servicecatalog_portfolio_share.example port-12344321:ACCOUNT:123456789012
```
