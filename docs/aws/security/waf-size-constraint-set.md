# Resource: aws_waf_size_constraint_set

Use the `aws_waf_size_constraint_set` resource to manage WAF size constraint sets.

## Basic Example

```yaml
resource:
  aws_waf_size_constraint_set:
    size_constraint_set:
      name: tfsize_constraints
      size_constraints:
        text_transformation: NONE
        comparison_operator: EQ
        size: 4096
        field_to_match:
          type: BODY
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) Name or description of the Size Constraint Set.
* `size_constraints` - (Optional) Parts of web requests that you want to inspect the size of.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the WAF Size Constraint Set.
* `arn` - Amazon Resource Name (ARN).

## Import

```bash
ytofu import aws_waf_size_constraint_set.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
