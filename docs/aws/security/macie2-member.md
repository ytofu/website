# Macie2 Member

Manage Macie2 Member resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_macie2_account:
    example:

resource:
  aws_macie2_member:
    example:
      account_id: AWS ACCOUNT ID
      email: EMAIL
      invite: true
      invitation_message: Message of the invitation
      invitation_disable_email_notification: true
      depends_on: 
        - ${aws_macie2_account.example}
```
