# Appconfig Configuration Profile

Manage Appconfig Configuration Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appconfig_configuration_profile:
    example:
      application_id: ${aws_appconfig_application.example.id}
      description: Example Configuration Profile
      name: example-configuration-profile-tf
      location_uri: hosted
      validator:
        content: ${aws_lambda_function.example.arn}
        type: LAMBDA
      tags:
        Type: AppConfig Configuration Profile
```
