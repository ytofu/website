# Notifications Organizational Unit Association

Manage Notifications Organizational Unit Association resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_organizations_organization:
    example:

resource:
  aws_notifications_notification_configuration:
    example:
      name: example-notification-config
      description: Example notification configuration

resource:
  aws_organizations_organizational_unit:
    example:
      name: example-ou
      parent_id: ${data.aws_organizations_organization.example.roots[0].id}

resource:
  time_sleep:
    wait:
      depends_on:
        - ${aws_organizations_organizational_unit.example}
        - ${aws_notifications_notification_configuration.example}
      create_duration: 5s

resource:
  aws_notifications_organizational_unit_association:
    example:
      depends_on: 
        - ${time_sleep.wait}
      organizational_unit_id: ${aws_organizations_organizational_unit.example.id}
      notification_configuration_arn: ${aws_notifications_notification_configuration.example.arn}
```

## Associate with Organization Root

```yaml
data:
  aws_organizations_organization:
    example:

resource:
  aws_notifications_notification_configuration:
    example:
      name: example-notification-config
      description: Example notification configuration

resource:
  aws_notifications_organizational_unit_association:
    example:
      organizational_unit_id: ${data.aws_organizations_organization.example.roots[0].id}
      notification_configuration_arn: ${aws_notifications_notification_configuration.example.arn}
```
