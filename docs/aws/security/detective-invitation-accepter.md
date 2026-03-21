# Detective Invitation Accepter

Manage Detective Invitation Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_detective_graph:
    primary:

resource:
  aws_detective_member:
    primary:
      account_id: ACCOUNT ID
      email_address: EMAIL
      graph_arn: ${aws_detective_graph.primary.graph_arn}
      message: Message of the invite

resource:
  aws_detective_invitation_accepter:
    member:
      graph_arn: ${aws_detective_graph.primary.graph_arn}
      depends_on: 
        - ${aws_detective_member.primary}
```
