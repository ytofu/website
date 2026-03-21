# Resource: aws_securityhub_invite_accepter



## Basic Example

```yaml
resource:
  aws_securityhub_account:
    example:

resource:
  aws_securityhub_member:
    example:
      account_id: 123456789012
      email: example@example.com
      invite: true

resource:
  aws_securityhub_account:
    invitee:

resource:
  aws_securityhub_invite_accepter:
    invitee:
      depends_on: 
        - ${aws_securityhub_account.invitee}
      master_id: ${aws_securityhub_member.example.master_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `master_id` - (Required) The account ID of the master Security Hub account whose invitation you're accepting.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `invitation_id` - The ID of the invitation.

## Import

```bash
ytofu import aws_securityhub_invite_accepter.example 123456789012
```
