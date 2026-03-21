# Securitylake Subscriber Notification

Manage Securitylake Subscriber Notification resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securitylake_subscriber_notification:
    example:
      subscriber_id: ${aws_securitylake_subscriber.example.id}
      configuration:
        sqs_notification_configuration:
```

## HTTPS Notification

```yaml
resource:
  aws_securitylake_subscriber_notification:
    example:
      subscriber_id: ${aws_securitylake_subscriber.example.id}
      configuration:
        https_notification_configuration:
          endpoint: ${aws_apigatewayv2_api.test.api_endpoint}
          target_role_arn: ${aws_iam_role.event_bridge.arn}
```
