# Resource: aws_guardduty_invite_accepter

Provides a resource to accept a pending GuardDuty invite on creation, ensure the detector has the correct primary account on read, and disassociate with the primary account upon removal.

## Basic Example

```yaml
resource:
  aws_guardduty_invite_accepter:
    member:
      depends_on: 
        - ${aws_guardduty_member.member}
      detector_id: ${aws_guardduty_detector.member.id}
      master_account_id: ${aws_guardduty_detector.primary.account_id}

  aws_guardduty_member:
    member:
      account_id: ${aws_guardduty_detector.member.account_id}
      detector_id: ${aws_guardduty_detector.primary.id}
      email: required@example.com
      invite: true

  aws_guardduty_detector:
    primary:

  aws_guardduty_detector:
    member:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `detector_id` - (Required) The detector ID of the member GuardDuty account.
* `master_account_id` - (Required) AWS account ID for primary account.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

- `create` - (Default `1m`)

## Import

```bash
ytofu import aws_guardduty_invite_accepter.member 00b00fd5aecc0ab60a708659477e9617
```
