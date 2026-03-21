# Route53 Query Log

Manage Route53 Query Log resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    aws_route53_example_com:
      name: "/aws/route53/${aws_route53_zone.example_com.name}"
      retention_in_days: 30

data:
  aws_iam_policy_document:
    route53-query-logging-policy:
      statement:
        actions:
          - "logs:CreateLogStream"
          - "logs:PutLogEvents"
        resources: 
          - "arn:aws:logs:*:*:log-group:/aws/route53/*"
        principals:
          identifiers: 
            - route53.amazonaws.com
          type: Service

resource:
  aws_cloudwatch_log_resource_policy:
    route53-query-logging-policy:
      policy_document: ${data.aws_iam_policy_document.route53-query-logging-policy.json}
      policy_name: route53-query-logging-policy

resource:
  aws_route53_zone:
    example_com:
      name: example.com

resource:
  aws_route53_query_log:
    example_com:
      depends_on: 
        - ${aws_cloudwatch_log_resource_policy.route53-query-logging-policy}
      cloudwatch_log_group_arn: ${aws_cloudwatch_log_group.aws_route53_example_com.arn}
      zone_id: ${aws_route53_zone.example_com.zone_id}
```
