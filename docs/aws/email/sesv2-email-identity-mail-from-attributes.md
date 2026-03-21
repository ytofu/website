# Sesv2 Email Identity Mail From Attributes

Manage Sesv2 Email Identity Mail From Attributes resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sesv2_email_identity:
    example:
      email_identity: example.com

resource:
  aws_sesv2_email_identity_mail_from_attributes:
    example:
      email_identity: ${aws_sesv2_email_identity.example.email_identity}
      behavior_on_mx_failure: REJECT_MESSAGE
      mail_from_domain: "subdomain.${aws_sesv2_email_identity.example.email_identity}"
```
