# Resource: aws_cloudwatch_contributor_managed_insight_rule

ytofu resource for managing an AWS CloudWatch Contributor Managed Insight Rule.

## Basic Example

```yaml
resource:
  aws_cloudwatch_contributor_managed_insight_rule:
    example:
      resource_arn: ${aws_vpc_endpoint_service.test.arn}
      template_name: VpcEndpointService-BytesByEndpointId-v1
      rule_state: DISABLED
```

## Argument Reference

The following arguments are required:

* `resource_arn` - (Required) ARN of an Amazon Web Services resource that has managed Contributor Insights rules.
* `template_name` - (Required) Template name for the managed Contributor Insights rule, as returned by ListManagedInsightRules.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rule_state` - (Optional) State of the rule. Valid values are `ENABLED` and `DISABLED`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Contributor Managed Insight Rule.

## Import

```bash
ytofu import aws_cloudwatch_contributor_managed_insight_rule.example contributor_managed_insight_rule-id-12345678
```
