# Resource: aws_cloudwatch_contributor_insight_rule

ytofu resource for managing an AWS CloudWatch Contributor Insight Rule.

## Basic Example

```yaml
resource:
  aws_cloudwatch_contributor_insight_rule:
    test:
      rule_name: testing
      rule_state: ENABLED
      rule_definition: "{\"Schema\":{\"Name\":\"CloudWatchLogRule\",\"Version\":1},\"AggregateOn\":\"Count\",\"Contribution\":{\"Filters\":[{\"In\":[\"some-keyword\"],\"Match\":\"$.message\"}],\"Keys\":[\"$.country\"]},\"LogFormat\":\"JSON\",\"LogGroupNames\":[\"/aws/lambda/api-prod\"]}"
```

## Argument Reference

The following arguments are required:

* `rule_definition` - (Required) Definition of the rule, as a JSON object. For details on the valid syntax, see [Contributor Insights Rule Syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/ContributorInsights-RuleSyntax.html).
* `rule_name` - (Required) Unique name of the rule.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rule_state` - (Optional) State of the rule. Valid values are `ENABLED` and `DISABLED`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `resource_arn` - ARN of the Contributor Insight Rule.

## Import

```bash
ytofu import aws_cloudwatch_contributor_insight_rule.example contributor_insight_rule-name
```
