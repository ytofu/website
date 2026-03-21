# Resource: aws_sesv2_email_identity_feedback_attributes

ytofu resource for managing an AWS SESv2 (Simple Email V2) Email Identity Feedback Attributes.

## Basic Example

```yaml
resource:
  aws_sesv2_email_identity:
    example:
      email_identity: example.com

  aws_sesv2_email_identity_feedback_attributes:
    example:
      email_identity: ${aws_sesv2_email_identity.example.email_identity}
      email_forwarding_enabled: true```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `email_identity` - (Required) The email identity.
* `email_forwarding_enabled` - (Optional) Sets the feedback forwarding configuration for the identity.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_sesv2_email_identity_feedback_attributes.example example.com
```
