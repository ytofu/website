# Resource: aws_route53_query_log

Provides a Route53 query logging configuration resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    aws_route53_example_com:
      name: "/aws/route53/${aws_route53_zone.example_com.name}"
      retention_in_days: 30

  aws_cloudwatch_log_resource_policy:
    route53-query-logging-policy:
      policy_document: ${data.aws_iam_policy_document.route53-query-logging-policy.json}
      policy_name: route53-query-logging-policy

  aws_route53_zone:
    example_com:
      name: example.com

  aws_route53_query_log:
    example_com:
      depends_on: 
        - ${aws_cloudwatch_log_resource_policy.route53-query-logging-policy}
      cloudwatch_log_group_arn: ${aws_cloudwatch_log_group.aws_route53_example_com.arn}
      zone_id: ${aws_route53_zone.example_com.zone_id}

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
          type: Service```

## Argument Reference

This resource supports the following arguments:

* `cloudwatch_log_group_arn` - (Required) CloudWatch log group ARN to send query logs.
* `zone_id` - (Required) Route53 hosted zone ID to enable query logs.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the Query Logging Config.
* `id` - The query logging configuration ID

## Import

```bash
ytofu import aws_route53_query_log.example_com xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
