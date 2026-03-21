# Quicksight Account Subscription

Manage Quicksight Account Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_account_subscription:
    subscription:
      account_name: quicksight-terraform
      authentication_method: IAM_AND_QUICKSIGHT
      edition: ENTERPRISE
      notification_email: notification@email.com
```
