# Resource: aws_inspector2_enabler

ytofu resource for enabling Amazon Inspector resource scans.

## Basic Example

```yaml
resource:
  aws_inspector2_enabler:
    example:
      account_ids: 
        - 123456789012
      resource_types: 
        - EC2
```

## For the Calling Account

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_inspector2_enabler:
    test:
      account_ids: 
        - ${data.aws_caller_identity.current.account_id}
      resource_types: 
        - ECR
        - EC2
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_ids` - (Required) Set of account IDs.
  Can contain one of: the Organization's Administrator Account, or one or more Member Accounts.
* `resource_types` - (Required) Type of resources to scan.
  Valid values are `EC2`, `ECR`, `LAMBDA`, `LAMBDA_CODE` and `CODE_REPOSITORY`.
  At least one item is required.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_inspector2_enabler.example 123456789012:234567890123-EC2:ECR
```
