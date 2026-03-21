# Networkflowmonitor Scope

Manage Networkflowmonitor Scope resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_networkflowmonitor_scope:
    example:
      target:
        region: us-east-1
        target_identifier:
          target_type: ACCOUNT
          target_id:
            account_id: ${data.aws_caller_identity.current.account_id}
      tags:
        Name: example
```
