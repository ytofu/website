# Resource: aws_sesv2_email_identity_mail_from_attributes

ytofu resource for managing an AWS SESv2 (Simple Email V2) Email Identity Mail From Attributes.

## Basic Example

```yaml
resource:
  aws_sesv2_email_identity:
    example:
      email_identity: example.com

  aws_sesv2_email_identity_mail_from_attributes:
    example:
      email_identity: ${aws_sesv2_email_identity.example.email_identity}
      behavior_on_mx_failure: REJECT_MESSAGE
      mail_from_domain: "subdomain.${aws_sesv2_email_identity.example.email_identity}"```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `email_identity` - (Required) The verified email identity.
* `behavior_on_mx_failure` - (Optional) The action to take if the required MX record isn't found when you send an email. Valid values: `USE_DEFAULT_VALUE`, `REJECT_MESSAGE`.
* `mail_from_domain` - (Optional) The custom MAIL FROM domain that you want the verified identity to use. Required if `behavior_on_mx_failure` is `REJECT_MESSAGE`.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_sesv2_email_identity_mail_from_attributes.example example.com
```
