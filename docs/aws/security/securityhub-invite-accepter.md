# Securityhub Invite Accepter

Manage Securityhub Invite Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_member:
    example:
      account_id: 123456789012
      email: example@example.com
      invite: true

resource:
  aws_securityhub_account:
    invitee:

resource:
  aws_securityhub_invite_accepter:
    invitee:
      depends_on: 
        - ${aws_securityhub_account.invitee}
      master_id: ${aws_securityhub_member.example.master_id}
```
