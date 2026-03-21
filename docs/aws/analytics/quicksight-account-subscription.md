# Resource: aws_quicksight_account_subscription

ytofu resource for managing an AWS QuickSight Account Subscription.

## Basic Example

```yaml
resource:
  aws_quicksight_account_subscription:
    subscription:
      account_name: quicksight-terraform
      authentication_method: IAM_AND_QUICKSIGHT
      edition: ENTERPRISE
      notification_email: notification@email.com
```

## Argument Reference

The following arguments are required:

* `account_name` - (Required) Name of your Amazon QuickSight account. This name is unique over all of AWS, and it appears only when users sign in.
* `authentication_method` - (Required) Method that you want to use to authenticate your Amazon QuickSight account. Currently, the valid values for this parameter are `IAM_AND_QUICKSIGHT`, `IAM_ONLY`, `IAM_IDENTITY_CENTER`, and `ACTIVE_DIRECTORY`.
* `edition` - (Required) Edition of Amazon QuickSight that you want your account to have. Currently, you can choose from `STANDARD`, `ENTERPRISE` or `ENTERPRISE_AND_Q`.
* `notification_email` - (Required) Email address that you want Amazon QuickSight to send notifications to regarding your Amazon QuickSight account or Amazon QuickSight subscription.

The following arguments are optional:

* `active_directory_name` - (Optional) Name of your Active Directory. This field is required if `ACTIVE_DIRECTORY` is the selected authentication method of the new Amazon QuickSight account.
* `admin_group` - (Optional) Admin group associated with your Active Directory or IAM Identity Center account. This field is required if `ACTIVE_DIRECTORY` or `IAM_IDENTITY_CENTER` is the selected authentication method of the new Amazon QuickSight account.
* `admin_pro_group` - (Optional) Admin PRO group associated with your Active Directory or IAM Identity Center account.
* `author_group` - (Optional) Author group associated with your Active Directory or IAM Identity Center account.
* `author_pro_group` - (Optional) Author PRO group associated with your Active Directory or IAM Identity Center account.
* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `contact_number` - (Optional) A 10-digit phone number for the author of the Amazon QuickSight account to use for future communications. This field is required if `ENTERPPRISE_AND_Q` is the selected edition of the new Amazon QuickSight account.
* `directory_id` - (Optional) Active Directory ID that is associated with your Amazon QuickSight account.
* `email_address` - (Optional) Email address of the author of the Amazon QuickSight account to use for future communications. This field is required if `ENTERPPRISE_AND_Q` is the selected edition of the new Amazon QuickSight account.
* `first_name` - (Optional) First name of the author of the Amazon QuickSight account to use for future communications. This field is required if `ENTERPPRISE_AND_Q` is the selected edition of the new Amazon QuickSight account.
* `iam_identity_center_instance_arn` - (Optional) The Amazon Resource Name (ARN) for the IAM Identity Center instance.
* `last_name` - (Optional) Last name of the author of the Amazon QuickSight account to use for future communications. This field is required if `ENTERPPRISE_AND_Q` is the selected edition of the new Amazon QuickSight account.
* `reader_group` - (Optional) Reader group associated with your Active Directory or IAM Identity Center account.
* `reader_pro_group` - (Optional) Reader PRO group associated with your Active Directory or IAM Identity Center account.
* `realm` - (Optional) Realm of the Active Directory that is associated with your Amazon QuickSight account.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `account_subscription_status` - Status of the Amazon QuickSight account's subscription.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_quicksight_account_subscription.example "012345678901"
```
