# Sesv2 Email Identity Feedback Attributes

Manage Sesv2 Email Identity Feedback Attributes resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sesv2_email_identity:
    example:
      email_identity: example.com

resource:
  aws_sesv2_email_identity_feedback_attributes:
    example:
      email_identity: ${aws_sesv2_email_identity.example.email_identity}
      email_forwarding_enabled: true
```
