# Resource: aws_accessanalyzer_archive_rule

ytofu resource for managing an AWS AccessAnalyzer Archive Rule.

## Basic Example

```yaml
resource:
  aws_accessanalyzer_archive_rule:
    example:
      analyzer_name: example-analyzer
      rule_name: example-rule
      filter:
        criteria: "condition.aws:UserId"
        eq: 
          - userid
      filter:
        criteria: error
        exists: true
      filter:
        criteria: isPublic
        eq: 
          - false
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `analyzer_name` - (Required) Analyzer name.
* `filter` - (Required) Filter criteria for the archive rule. See [Filter](#filter) for more details.
* `rule_name` - (Required) Rule name.

### Filter

**Note** One comparator must be included with each filter.

* `criteria` - (Required) Filter criteria.
* `contains` - (Optional) Contains comparator.
* `eq` - (Optional) Equals comparator.
* `exists` - (Optional) Boolean comparator.
* `neq` - (Optional) Not Equals comparator.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Resource ID in the format: `analyzer_name/rule_name`.

## Import

```bash
ytofu import aws_accessanalyzer_archive_rule.example example-analyzer/example-rule
```
