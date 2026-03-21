# Resource: aws_costoptimizationhub_preferences

ytofu resource for managing AWS Cost Optimization Hub Preferences.

## Basic Example

```yaml
resource:
  aws_costoptimizationhub_preferences:
    example:
```

## Usage with all the arguments

```yaml
resource:
  aws_costoptimizationhub_preferences:
    example:
      member_account_discount_visibility: None
      savings_estimation_mode: AfterDiscounts
```

## Argument Reference

The following arguments are optional:

* `member_account_discount_visibility` - (Optional) Customize whether the member accounts can see the "After Discounts" savings estimates. Valid values are `All` and `None`. Default value is `All`.
* `savings_estimation_mode` - (Optional) Customize how estimated monthly savings are calculated. Valid values are `BeforeDiscounts` and `AfterDiscounts`. Default value is `BeforeDiscounts`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Unique identifier for the preferences resource. Since preferences are for the entire account, this will be the 12-digit account id.

## Import

```bash
ytofu import aws_costoptimizationhub_preferences.example 111222333444
```
