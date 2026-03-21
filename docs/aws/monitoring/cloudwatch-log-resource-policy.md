# Cloudwatch Log Resource Policy

Manage Cloudwatch Log Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    elasticsearch-log-publishing-policy:
      statement:
        actions:
          - "logs:CreateLogStream"
          - "logs:PutLogEvents"
          - "logs:PutLogEventsBatch"
        resources: 
          - "arn:aws:logs:*"
        principals:
          identifiers: 
            - es.amazonaws.com
          type: Service

resource:
  aws_cloudwatch_log_resource_policy:
    elasticsearch-log-publishing-policy:
      policy_document: ${data.aws_iam_policy_document.elasticsearch-log-publishing-policy.json}
      policy_name: elasticsearch-log-publishing-policy
```

## Route53 Query Logging

```yaml
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
```
