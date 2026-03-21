# Securityhub Action Target

Manage Securityhub Action Target resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_action_target:
    example:
      depends_on: 
        - ${aws_securityhub_account.example}
      name: Send notification to chat
      identifier: SendToChat
      description: This is custom action sends selected findings to chat
```
