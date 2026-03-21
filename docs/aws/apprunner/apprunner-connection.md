# Apprunner Connection

Manage Apprunner Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_connection:
    example:
      connection_name: example
      provider_type: GITHUB
      tags:
        Name: example-apprunner-connection
```
