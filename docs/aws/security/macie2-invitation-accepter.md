# Macie2 Invitation Accepter

Manage Macie2 Invitation Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_macie2_account:
    primary:

resource:
  aws_macie2_account:
    member:

resource:
  aws_macie2_member:
    primary:
      account_id: ACCOUNT ID
      email: EMAIL
      invite: true
      invitation_message: Message of the invite
      depends_on: 
        - ${aws_macie2_account.primary}

resource:
  aws_macie2_invitation_accepter:
    member:
      administrator_account_id: ADMINISTRATOR ACCOUNT ID
      depends_on: 
        - ${aws_macie2_member.primary}
```
