# Resource: aws_ses_receipt_filter

Provides an SES receipt filter resource

## Basic Example

```yaml
resource:
  aws_ses_receipt_filter:
    filter:
      name: block-spammer
      cidr: 10.10.10.10
      policy: Block
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the filter
* `cidr` - (Required) The IP address or address range to filter, in CIDR notation
* `policy` - (Required) Block or Allow

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The SES receipt filter name.
* `arn` - The SES receipt filter ARN.

## Import

```bash
ytofu import aws_ses_receipt_filter.test some-filter
```
