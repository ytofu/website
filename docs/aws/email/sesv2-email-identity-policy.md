# Sesv2 Email Identity Policy

Manage Sesv2 Email Identity Policy resources using ytofu YAML.

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
