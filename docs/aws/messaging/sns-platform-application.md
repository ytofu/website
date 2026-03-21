# SNS Platform Application

Manage SNS Platform Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sns_platform_application:
    apns_application:
      name: apns_application
      platform: APNS
      platform_credential: <APNS PRIVATE KEY>
      platform_principal: <APNS CERTIFICATE>
```

## Apple Push Notification Service (APNS) using token-based authentication

```yaml
resource:
  aws_sns_platform_application:
    apns_application:
      name: apns_application
      platform: APNS
      platform_credential: <APNS SIGNING KEY>
      platform_principal: <APNS SIGNING KEY ID>
      apple_platform_team_id: <APPLE TEAM ID>
      apple_platform_bundle_id: <APPLE BUNDLE ID>
```

## Google Cloud Messaging (GCM)

```yaml
resource:
  aws_sns_platform_application:
    gcm_application:
      name: gcm_application
      platform: GCM
      platform_credential: <GCM API KEY>
```
