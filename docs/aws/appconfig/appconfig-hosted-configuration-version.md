# Appconfig Hosted Configuration Version

Manage Appconfig Hosted Configuration Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appconfig_hosted_configuration_version:
    example:
      application_id: ${aws_appconfig_application.example.id}
      configuration_profile_id: ${aws_appconfig_configuration_profile.example.configuration_profile_id}
      description: Example Freeform Hosted Configuration Version
      content_type: application/json
      content: '{ "foo": "bar", "fruit": ["apple", "pear", "orange"], "isThingEnabled": true }'
```

## Feature Flags

```yaml
resource:
  aws_appconfig_hosted_configuration_version:
    example:
      application_id: ${aws_appconfig_application.example.id}
      configuration_profile_id: ${aws_appconfig_configuration_profile.example.configuration_profile_id}
      description: Example Feature Flag Configuration Version
      content_type: application/json
      content: '{ flags : { foo : { name : "foo", _deprecation : { "status" : "planned" } }, bar : { name : "bar", attributes : { someAttribute : { constraints : { type : "string", required : true } }, someOtherAttribute : { constraints : { type : "number", required : true } } } } }, values : { foo : { enabled : "true", }, bar : { enabled : "true", someAttribute : "Hello World", someOtherAttribute : 123 } }, version : "1" }'
```

## Multi-variant Feature Flags

```yaml
resource:
  aws_appconfig_hosted_configuration_version:
    example:
      application_id: ${aws_appconfig_application.example.id}
      configuration_profile_id: ${aws_appconfig_configuration_profile.example.configuration_profile_id}
      description: Example Multi-variant Feature Flag Configuration Version
      content_type: application/json
      content: '{ "flags": { "loggingenabled": { "name": "loggingEnabled" } }, "values": { "loggingenabled": { "_variants": concat([ for user_id in var.appcfg_enableLogging_userIds : { # Flat list of userIds "enabled": true, "name": "usersWithLoggingEnabled_${user_id}", "rule": "(or (eq $userId \"${user_id}\"))" } ], [ { "enabled": false, "name": "Default" } ]) } }, "version": "1" }'
```
