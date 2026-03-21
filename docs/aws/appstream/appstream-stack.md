# Appstream Stack

Manage Appstream Stack resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appstream_stack:
    example:
      name: stack name
      description: stack description
      display_name: stack display name
      feedback_url: "http://your-domain/feedback"
      redirect_url: "http://your-domain/redirect"
      storage_connectors:
        connector_type: HOMEFOLDERS
      user_settings:
        action: AUTO_TIME_ZONE_REDIRECTION
        permission: DISABLED
      user_settings:
        action: CLIPBOARD_COPY_FROM_LOCAL_DEVICE
        permission: ENABLED
      user_settings:
        action: CLIPBOARD_COPY_TO_LOCAL_DEVICE
        permission: ENABLED
      user_settings:
        action: DOMAIN_PASSWORD_SIGNIN
        permission: ENABLED
      user_settings:
        action: DOMAIN_SMART_CARD_SIGNIN
        permission: DISABLED
      user_settings:
        action: FILE_DOWNLOAD
        permission: ENABLED
      user_settings:
        action: FILE_UPLOAD
        permission: ENABLED
      user_settings:
        action: PRINTING_TO_LOCAL_DEVICE
        permission: ENABLED
      application_settings:
        enabled: true
        settings_group: SettingsGroup
      tags:
        TagName: TagValue
```
