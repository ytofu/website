# Resource: aws_vpc_block_public_access_options

ytofu resource for managing an AWS VPC Block Public Access Options.

## Basic Example

```yaml
resource:
  aws_vpc_block_public_access_options:
    example:
      internet_gateway_block_mode: block-bidirectional
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `internet_gateway_block_mode` - (Required) Block mode. Needs to be one of `block-bidirectional`, `block-ingress`, `off`. If this resource is deleted, then this value will be set to `off` in the AWS account and region.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `aws_account_id` - The AWS account id to which these options apply.
* `aws_region` - The AWS region to which these options apply.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_vpc_block_public_access_options.example us-east-1
```
