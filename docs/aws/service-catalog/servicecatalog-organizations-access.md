# Resource: aws_servicecatalog_organizations_access

Manages Service Catalog AWS Organizations Access, a portfolio sharing feature through AWS Organizations. This allows Service Catalog to receive updates on your organization in order to sync your shares with the current structure. This resource will prompt AWS to set `organizations:EnableAWSServiceAccess` on your behalf so that your shares can be in sync with any changes in your AWS Organizations structure.

## Basic Example

```yaml
resource:
  aws_servicecatalog_organizations_access:
    example:
      enabled: true
```

## Argument Reference

The following arguments are required:

* `enabled` - (Required) Whether to enable AWS Organizations access.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Account ID for the account using the resource.

## Timeouts

Configuration options:

- `read` - (Default `10m`)
