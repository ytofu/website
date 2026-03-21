# Resource: aws_config_aggregate_authorization

Manages an AWS Config Aggregate Authorization

## Basic Example

```yaml
resource:
  aws_config_aggregate_authorization:
    example:
      account_id: 123456789012
      authorized_aws_region: eu-west-2
```

## Argument Reference

This resource supports the following arguments:

* `account_id` - (Required) Account ID.
* `authorized_aws_region` - (Optional) The region authorized to collect aggregated data.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the authorization
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_config_aggregate_authorization.example 123456789012:us-east-1
```
