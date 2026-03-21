# Quicksight Account Settings

Manage Quicksight Account Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_account_subscription:
    subscription:
      account_name: quicksight-terraform
      authentication_method: IAM_AND_QUICKSIGHT
      edition: ENTERPRISE
      notification_email: notification@email.com

resource:
  aws_quicksight_account_settings:
    example:
      termination_protection_enabled: false
      depends_on: 
        - ${aws_quicksight_account_subscription.subscription}
```
