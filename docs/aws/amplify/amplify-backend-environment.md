# Amplify Backend Environment

Manage Amplify Backend Environment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_amplify_app:
    example:
      name: example

resource:
  aws_amplify_backend_environment:
    example:
      app_id: ${aws_amplify_app.example.id}
      environment_name: example
      deployment_artifacts: app-example-deployment
      stack_name: amplify-app-example
```
