# Resource: aws_ses_receipt_rule_set

Provides an SES receipt rule set resource.

## Basic Example

```yaml
resource:
  aws_ses_receipt_rule_set:
    main:
      rule_set_name: primary-rules
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rule_set_name` - (Required) Name of the rule set.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - SES receipt rule set ARN.
* `id` - SES receipt rule set name.

## Import

```bash
ytofu import aws_ses_receipt_rule_set.my_rule_set my_rule_set_name
```
