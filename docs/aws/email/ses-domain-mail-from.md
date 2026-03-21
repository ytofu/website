# SES Domain Mail From

Manage SES Domain Mail From resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ses_domain_mail_from:
    example:
      domain: ${aws_ses_domain_identity.example.domain}
      mail_from_domain: "bounce.${aws_ses_domain_identity.example.domain}"

resource:
  aws_ses_domain_identity:
    example:
      domain: example.com

resource:
  aws_route53_record:
    example_ses_domain_mail_from_mx:
      zone_id: ${aws_route53_zone.example.id}
      name: ${aws_ses_domain_mail_from.example.mail_from_domain}
      type: MX
      ttl: 600
      records: 
        - 10 feedback-smtp.us-east-1.amazonses.com

resource:
  aws_route53_record:
    example_ses_domain_mail_from_txt:
      zone_id: ${aws_route53_zone.example.id}
      name: ${aws_ses_domain_mail_from.example.mail_from_domain}
      type: TXT
      ttl: 600
      records: 
        - "v=spf1 include:amazonses.com ~all"
```

## Email Identity MAIL FROM

```yaml
resource:
  aws_ses_email_identity:
    example:
      email: user@example.com

resource:
  aws_ses_domain_mail_from:
    example:
      domain: ${aws_ses_email_identity.example.email}
      mail_from_domain: mail.example.com
```
