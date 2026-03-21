# Guardduty Invite Accepter

Manage Guardduty Invite Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_guardduty_invite_accepter:
    member:
      depends_on: 
        - ${aws_guardduty_member.member}
      detector_id: ${aws_guardduty_detector.member.id}
      master_account_id: ${aws_guardduty_detector.primary.account_id}

resource:
  aws_guardduty_member:
    member:
      account_id: ${aws_guardduty_detector.member.account_id}
      detector_id: ${aws_guardduty_detector.primary.id}
      email: required@example.com
      invite: true

resource:
  aws_guardduty_detector:
    primary:

resource:
  aws_guardduty_detector:
    member:
```
