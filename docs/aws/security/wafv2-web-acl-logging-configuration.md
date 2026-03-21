# Wafv2 Web Acl Logging Configuration

Manage Wafv2 Web Acl Logging Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_wafv2_web_acl_logging_configuration:
    example:
      log_destination_configs: 
        - ${aws_kinesis_firehose_delivery_stream.example.arn}
      resource_arn: ${aws_wafv2_web_acl.example.arn}
      redacted_fields:
        single_header:
          name: user-agent
```

## With Logging Filter

```yaml
resource:
  aws_wafv2_web_acl_logging_configuration:
    example:
      log_destination_configs: 
        - ${aws_kinesis_firehose_delivery_stream.example.arn}
      resource_arn: ${aws_wafv2_web_acl.example.arn}
      logging_filter:
        default_behavior: KEEP
        filter:
          behavior: DROP
          condition:
            action_condition:
              action: COUNT
          condition:
            label_name_condition:
              label_name: "awswaf:111122223333:rulegroup:testRules:LabelNameZ"
          requirement: MEETS_ALL
        filter:
          behavior: KEEP
          condition:
            action_condition:
              action: ALLOW
          requirement: MEETS_ANY
```

## With CloudWatch Log Group and managed CloudWatch Log Resource Policy

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: aws-waf-logs-some-uniq-suffix

resource:
  aws_wafv2_web_acl_logging_configuration:
    example:
      log_destination_configs: 
        - ${aws_cloudwatch_log_group.example.arn}
      resource_arn: ${aws_wafv2_web_acl.example.arn}

resource:
  aws_cloudwatch_log_resource_policy:
    example:
      policy_document: ${data.aws_iam_policy_document.example.json}
      policy_name: webacl-policy-uniq-name

data:
  aws_iam_policy_document:
    example:
      version: 2012-10-17
      statement:
        effect: Allow
        principals:
          identifiers: 
            - delivery.logs.amazonaws.com
          type: Service
        actions: 
          - "logs:CreateLogStream"
          - "logs:PutLogEvents"
        resources: 
          - "${aws_cloudwatch_log_group.example.arn}:*"
        condition:
          test: ArnLike
          values: 
            - "arn:aws:logs:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:*"
        condition:
          test: StringEquals
          values: 
            - string-value

data:
  aws_region:
    current:

data:
  aws_caller_identity:
    current:
```
