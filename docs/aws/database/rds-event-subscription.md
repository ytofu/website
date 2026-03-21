# RDS Event Subscription

Subscribe to RDS events using ytofu YAML.

## Basic Event Subscription

```yaml
resource:
  aws_sns_topic:
    default:
      name: rds-events

  aws_db_event_subscription:
    default:
      name: rds-event-sub
      sns_topic: ${aws_sns_topic.default.arn}
      source_type: db-instance
      source_ids:
        - ${aws_db_instance.default.identifier}
      event_categories:
        - availability
        - deletion
        - failover
        - failure
        - low storage
        - maintenance
        - notification
        - read replica
        - recovery
        - restoration
```
