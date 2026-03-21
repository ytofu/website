# Guardduty Member

Manage Guardduty Member resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_guardduty_detector:
    primary:
      enable: true

resource:
  aws_guardduty_detector:
    member:
      enable: true

resource:
  aws_guardduty_member:
    member:
      account_id: ${aws_guardduty_detector.member.account_id}
      detector_id: ${aws_guardduty_detector.primary.id}
      email: required@example.com
      invite: true
      invitation_message: please accept guardduty invitation
```
