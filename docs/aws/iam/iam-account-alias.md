# Resource: aws_iam_account_alias



## Basic Example

```yaml
resource:
  aws_iam_account_alias:
    alias:
      account_alias: my-account-alias
```

## Argument Reference

This resource supports the following arguments:

* `account_alias` - (Required) The account alias

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_account_alias.alias my-account-alias
```
