# Resource: aws_wafregional_size_constraint_set

Provides a WAF Regional Size Constraint Set Resource for use with Application Load Balancer.

## Basic Example

```yaml
resource:
  aws_wafregional_size_constraint_set:
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

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name or description of the Size Constraint Set.
* `size_constraints` - (Optional) Specifies the parts of web requests that you want to inspect the size of.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF Size Constraint Set.

## Import

```bash
ytofu import aws_wafregional_size_constraint_set.size_constraint_set a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
