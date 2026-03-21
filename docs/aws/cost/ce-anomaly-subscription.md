# Ce Anomaly Subscription

Manage Ce Anomaly Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ce_anomaly_monitor:
    test:
      name: AWSServiceMonitor
      monitor_type: DIMENSIONAL
      monitor_dimension: SERVICE

resource:
  aws_ce_anomaly_subscription:
    test:
      name: DAILYSUBSCRIPTION
      frequency: DAILY
      monitor_arn_list:
        - ${aws_ce_anomaly_monitor.test.arn}
      subscriber:
        type: EMAIL
        address: abc@example.com
      threshold_expression:
        dimension:
          key: ANOMALY_TOTAL_IMPACT_ABSOLUTE
          match_options: 
            - GREATER_THAN_OR_EQUAL
          values: 
            - 100
```

## Threshold Expression Example

```yaml
resource:
  aws_ce_anomaly_subscription:
    test:
      name: AWSServiceMonitor
      frequency: DAILY
      monitor_arn_list:
        - ${aws_ce_anomaly_monitor.test.arn}
      subscriber:
        type: EMAIL
        address: abc@example.com
      threshold_expression:
        dimension:
          key: ANOMALY_TOTAL_IMPACT_PERCENTAGE
          match_options: 
            - GREATER_THAN_OR_EQUAL
          values: 
            - 100
```

## SNS Example

```yaml
resource:
  aws_sns_topic:
    cost_anomaly_updates:
      name: CostAnomalyUpdates

data:
  aws_iam_policy_document:
    sns_topic_policy:
      policy_id: __default_policy_ID
      statement:
        sid: AWSAnomalyDetectionSNSPublishingPermissions
        actions:
          - "SNS:Publish"
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - costalerts.amazonaws.com
        resources:
          - ${aws_sns_topic.cost_anomaly_updates.arn}
      statement:
        sid: __default_statement_ID
        actions:
          - "SNS:Subscribe"
          - "SNS:SetTopicAttributes"
          - "SNS:RemovePermission"
          - "SNS:Receive"
          - "SNS:Publish"
          - "SNS:ListSubscriptionsByTopic"
          - "SNS:GetTopicAttributes"
          - "SNS:DeleteTopic"
          - "SNS:AddPermission"
        condition:
          test: StringEquals
          values:
            - example-account_id
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "*"
        resources:
          - ${aws_sns_topic.cost_anomaly_updates.arn}

resource:
  aws_sns_topic_policy:
    default:
      arn: ${aws_sns_topic.cost_anomaly_updates.arn}
      policy: ${data.aws_iam_policy_document.sns_topic_policy.json}

resource:
  aws_ce_anomaly_monitor:
    anomaly_monitor:
      name: AWSServiceMonitor
      monitor_type: DIMENSIONAL
      monitor_dimension: SERVICE

resource:
  aws_ce_anomaly_subscription:
    realtime_subscription:
      name: RealtimeAnomalySubscription
      frequency: IMMEDIATE
      monitor_arn_list:
        - ${aws_ce_anomaly_monitor.anomaly_monitor.arn}
      subscriber:
        type: SNS
        address: ${aws_sns_topic.cost_anomaly_updates.arn}
      depends_on:
        - ${aws_sns_topic_policy.default}
```
