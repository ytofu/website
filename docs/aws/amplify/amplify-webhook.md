# Amplify Webhook

Manage Amplify Webhook resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_amplify_app:
    example:
      name: app

resource:
  aws_amplify_branch:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: master

resource:
  aws_amplify_webhook:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: ${aws_amplify_branch.master.branch_name}
      description: triggermaster
```
