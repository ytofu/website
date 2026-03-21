# Cloudwatch Contributor Managed Insight Rule

Manage Cloudwatch Contributor Managed Insight Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_contributor_managed_insight_rule:
    example:
      resource_arn: ${aws_vpc_endpoint_service.test.arn}
      template_name: VpcEndpointService-BytesByEndpointId-v1
      rule_state: DISABLED
```
