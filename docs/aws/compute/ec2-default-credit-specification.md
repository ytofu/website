# Resource: aws_ec2_default_credit_specification

ytofu resource for managing an AWS EC2 (Elastic Compute Cloud) Default Credit Specification.

## Basic Example

```yaml
resource:
  aws_ec2_default_credit_specification:
    example:
      instance_family: t2
      cpu_credits: standard
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cpu_credits` - (Required) Credit option for CPU usage of the instance family. Valid values: `standard`, `unlimited`.
* `instance_family` - (Required) Instance family. Valid values are `t2`, `t3`, `t3a`, `t4g`.

## Attribute Reference

This data source exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
