# Quicksight Folder

Manage Quicksight Folder resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_folder:
    example:
      folder_id: example-id
      name: example-name
```

## With Permissions

```yaml
resource:
  aws_quicksight_folder:
    example:
      folder_id: example-id
      name: example-name
      permissions:
        actions:
          - "quicksight:CreateFolder"
          - "quicksight:DescribeFolder"
          - "quicksight:UpdateFolder"
          - "quicksight:DeleteFolder"
          - "quicksight:CreateFolderMembership"
          - "quicksight:DeleteFolderMembership"
          - "quicksight:DescribeFolderPermissions"
          - "quicksight:UpdateFolderPermissions"
        principal: ${aws_quicksight_user.example.arn}
```

## With Parent Folder

```yaml
resource:
  aws_quicksight_folder:
    parent:
      folder_id: parent-id
      name: parent-name

resource:
  aws_quicksight_folder:
    example:
      folder_id: example-id
      name: example-name
      parent_folder_arn: ${aws_quicksight_folder.parent.arn}
```
