# Resource: aws_macie2_invitation_accepter

Provides a resource to manage an [Amazon Macie Invitation Accepter](https://docs.aws.amazon.com/macie/latest/APIReference/invitations-accept.html).

## Basic Example

```yaml
resource:
  aws_macie2_account:
    primary:

  aws_macie2_account:
    member:

  aws_macie2_member:
    primary:
      account_id: ACCOUNT ID
      email: EMAIL
      invite: true
      invitation_message: Message of the invite
      depends_on: 
        - ${aws_macie2_account.primary}

  aws_macie2_invitation_accepter:
    member:
      administrator_account_id: ADMINISTRATOR ACCOUNT ID
      depends_on: 
        - ${aws_macie2_member.primary}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `administrator_account_id` - (Required) The AWS account ID for the account that sent the invitation.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The unique identifier (ID) of the macie invitation accepter.
* `invitation_id` - The unique identifier for the invitation.

## Import

```bash
ytofu import aws_macie2_invitation_accepter.example 123456789012
```
