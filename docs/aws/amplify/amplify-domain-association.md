# Amplify Domain Association

Manage Amplify Domain Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_amplify_app:
    example:
      name: app
      custom_rule:
        source: "https://example.com"
        status: 302
        target: "https://www.example.com"

resource:
  aws_amplify_branch:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: master

resource:
  aws_amplify_domain_association:
    example:
      app_id: ${aws_amplify_app.example.id}
      domain_name: example.com
      sub_domain:
        branch_name: ${aws_amplify_branch.master.branch_name}
        prefix: 
      sub_domain:
        branch_name: ${aws_amplify_branch.master.branch_name}
        prefix: www
```
