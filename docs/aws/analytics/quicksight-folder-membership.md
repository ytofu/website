# Resource: aws_quicksight_folder_membership

ytofu resource for managing an AWS QuickSight Folder Membership.

## Basic Example

```yaml
resource:
  aws_quicksight_folder_membership:
    example:
      folder_id: ${aws_quicksight_folder.example.folder_id}
      member_type: DATASET
      member_id: ${aws_quicksight_data_set.example.data_set_id}
```

## Argument Reference

The following arguments are required:

* `folder_id` - (Required, Forces new resource) Identifier for the folder.
* `member_id` - (Required, Forces new resource) ID of the asset (the dashboard, analysis, or dataset).
* `member_type` - (Required, Forces new resource) Type of the member. Valid values are `ANALYSIS`, `DASHBOARD`, and `DATASET`.

The following arguments are optional:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A comma-delimited string joining AWS account ID, folder ID, member type, and member ID.

## Import

```bash
ytofu import aws_quicksight_folder_membership.example 123456789012,example-folder,DATASET,example-dataset
```
