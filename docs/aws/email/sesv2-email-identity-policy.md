# Resource: aws_sesv2_email_identity_policy

ytofu resource for managing an AWS SESv2 (Simple Email V2) Email Identity Policy.

## Basic Example

```yaml
resource:
  aws_sesv2_email_identity:
    example:
      email_identity: testing@example.com

resource:
  aws_sesv2_email_identity_policy:
    example:
      email_identity: ${aws_sesv2_email_identity.example.email_identity}
      policy_name: example
      policy: |
        {
        "Id":"ExampleAuthorizationPolicy",
        "Version":"2012-10-17",
        "Statement":[
        {
        "Sid":"AuthorizeIAMUser",
        "Effect":"Allow",
        "Resource":"${aws_sesv2_email_identity.example.arn}",
        "Principal":{
        "AWS":[
        "arn:aws:iam::123456789012:user/John",
        "arn:aws:iam::123456789012:user/Jane"
        ]
        },
        "Action":[
        "ses:DeleteEmailIdentity",
        "ses:PutEmailIdentityDkimSigningAttributes"
        ]
        }
        ]
        }
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `email_identity` - (Required) The email identity.
* `policy_name` - (Required) - The name of the policy.
* `policy` - (Required) - The text of the policy in JSON format.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_sesv2_email_identity_policy.example example_email_identity|example_policy_name
```
