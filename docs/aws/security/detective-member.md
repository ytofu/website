# Detective Member

Manage Detective Member resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_detective_graph:
    example:

resource:
  aws_detective_member:
    example:
      account_id: AWS ACCOUNT ID
      email_address: EMAIL
      graph_arn: ${aws_detective_graph.example.graph_arn}
      message: Message of the invitation
      disable_email_notification: true
```
