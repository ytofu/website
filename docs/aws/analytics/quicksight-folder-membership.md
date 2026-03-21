# Quicksight Folder Membership

Manage Quicksight Folder Membership resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_folder_membership:
    example:
      folder_id: ${aws_quicksight_folder.example.folder_id}
      member_type: DATASET
      member_id: ${aws_quicksight_data_set.example.data_set_id}
```
