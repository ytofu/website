# Resource: aws_ses_email_identity

Provides an SES email identity resource

## Basic Example

```yaml
resource:
  aws_ses_email_identity:
    example:
      email: email@example.com
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `email` - (Required) The email address to assign to SES.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the email identity.

## Import

```bash
ytofu import aws_ses_email_identity.example email@example.com
```
