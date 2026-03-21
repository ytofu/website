# Resource: aws_guardduty_member

Provides a resource to manage a GuardDuty member. To accept invitations in member accounts, see the `aws_guardduty_invite_accepter` resource.

## Basic Example

```yaml
resource:
  aws_guardduty_detector:
    primary:
      enable: true

  aws_guardduty_detector:
    member:
      enable: true

  aws_guardduty_member:
    member:
      account_id: ${aws_guardduty_detector.member.account_id}
      detector_id: ${aws_guardduty_detector.primary.id}
      email: required@example.com
      invite: true
      invitation_message: please accept guardduty invitation```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account_id` - (Required) AWS account ID for member account.
* `detector_id` - (Required) The detector ID of the GuardDuty account where you want to create member accounts.
* `email` - (Required) Email address for member account.
* `invite` - (Optional) Boolean whether to invite the account to GuardDuty as a member. Defaults to `false`. To detect if an invitation needs to be (re-)sent, the ytofu state value is `true` based on a `relationship_status` of `Disabled`, `Enabled`, `Invited`, or `EmailVerificationInProgress`.
* `invitation_message` - (Optional) Message for invitation.
* `disable_email_notification` - (Optional) Boolean whether an email notification is sent to the accounts. Defaults to `false`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `relationship_status` - The status of the relationship between the member account and its primary account. More information can be found in [Amazon GuardDuty API Reference](https://docs.aws.amazon.com/guardduty/latest/ug/get-members.html).

## Timeouts

Configuration options:

- `create` - (Default `1m`)
- `update` - (Default `1m`)

## Import

```bash
ytofu import aws_guardduty_member.MyMember 00b00fd5aecc0ab60a708659477e9617:123456789012
```
