# Resource: aws_cloudwatch_log_resource_policy

Provides a resource to manage a CloudWatch log resource policy.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy_document` - (Required) Details of the resource policy, including the identity of the principal that is enabled to put logs to this account. This is formatted as a JSON string. Maximum length of 5120 characters.
* `policy_name` - (Optional) Name of the resource policy. Exactly one of `policy_name` or `resource_arn` must be specified and this argument is required for account-scoped policies. Note that the number of resource policies without `resource_arn` is limited to 10 per region.
* `resource_arn` - (Optional) ARN of the CloudWatch Logs resource to which the resource policy is attached. Exactly one of `policy_name` or `resource_arn` must be specified and this argument is required for resource-scoped policies. Only one policy can be attached per log group resource ARN.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the CloudWatch log resource policy when `resource_arn` is not specified, or the ARN of the CloudWatch log group when `resource_arn` is specified.
* `policy_scope` - Scope of the resource policy (`ACCOUNT` or `RESOURCE`).
* `revision_id` - Revision ID of the resource policy. Only populated for resource-scoped policies.

## Import

```bash
ytofu import aws_cloudwatch_log_resource_policy.my_policy_account_scoped my_policy
```
