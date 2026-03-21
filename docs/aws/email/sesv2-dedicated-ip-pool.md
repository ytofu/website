# Resource: aws_sesv2_dedicated_ip_pool

ytofu resource for managing an AWS SESv2 (Simple Email V2) Dedicated IP Pool.

## Basic Example

```yaml
resource:
  aws_sesv2_dedicated_ip_pool:
    example:
      pool_name: my-pool
```

## Managed Pool

```yaml
resource:
  aws_sesv2_dedicated_ip_pool:
    example:
      pool_name: my-managed-pool
      scaling_mode: MANAGED
```

## Argument Reference

The following arguments are required:

* `pool_name` - (Required) Name of the dedicated IP pool.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `scaling_mode` - (Optional) IP pool scaling mode. Valid values: `STANDARD`, `MANAGED`. If omitted, the AWS API will default to a standard pool.
* `tags` - (Optional) A map of tags to assign to the pool. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Dedicated IP Pool.

## Import

```bash
ytofu import aws_sesv2_dedicated_ip_pool.example my-pool
```
