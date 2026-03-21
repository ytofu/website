# Resource: aws_quicksight_namespace

ytofu resource for managing an AWS QuickSight Namespace.

## Basic Example

```yaml
resource:
  aws_quicksight_namespace:
    example:
      namespace: example
```

## Argument Reference

The following arguments are required:

* `namespace` - (Required) Name of the namespace.

The following arguments are optional:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `identity_store` - (Optional) User identity directory type. Defaults to `QUICKSIGHT`, the only current valid value.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Namespace.
* `capacity_region` - Namespace AWS Region.
* `creation_status` - Creation status of the namespace.
* `id` - A comma-delimited string joining AWS account ID and namespace.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `2m`)
* `delete` - (Default `2m`)

## Import

```bash
ytofu import aws_quicksight_namespace.example 123456789012,example
```
