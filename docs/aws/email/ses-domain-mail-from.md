# Resource: aws_ses_domain_mail_from

Provides an SES domain MAIL FROM resource.

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

## Argument Reference

The following arguments are required:

* `domain` - (Required) Verified domain name or email identity to generate DKIM tokens for.
* `mail_from_domain` - (Required) Subdomain (of above domain) which is to be used as MAIL FROM address (Required for DMARC validation)

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `behavior_on_mx_failure` - (Optional) The action that you want Amazon SES to take if it cannot successfully read the required MX record when you send an email. Defaults to `UseDefaultValue`. See the [SES API documentation](https://docs.aws.amazon.com/ses/latest/APIReference/API_SetIdentityMailFromDomain.html) for more information.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The domain name.

## Import

```bash
ytofu import aws_ses_domain_mail_from.example example.com
```
