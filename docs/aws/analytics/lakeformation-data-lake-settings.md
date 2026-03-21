# Lakeformation Data Lake Settings

Manage Lakeformation Data Lake Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      admins: 
        - ${aws_iam_user.test.arn}
        - ${aws_iam_role.test.arn}
```

## Create Default Permissions

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      admins: 
        - ${aws_iam_user.test.arn}
        - ${aws_iam_role.test.arn}
      create_database_default_permissions:
        permissions: 
          - SELECT
          - ALTER
          - DROP
        principal: ${aws_iam_user.test.arn}
      create_table_default_permissions:
        permissions: 
          - ALL
        principal: ${aws_iam_role.test.arn}
```

## Enable EMR access to LakeFormation resources

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      admins: 
        - ${aws_iam_user.test.arn}
        - ${aws_iam_role.test.arn}
      create_database_default_permissions:
        permissions: 
          - SELECT
          - ALTER
          - DROP
        principal: ${aws_iam_user.test.arn}
      create_table_default_permissions:
        permissions: 
          - ALL
        principal: ${aws_iam_role.test.arn}
      allow_external_data_filtering: true
      external_data_filtering_allow_list: 
        - ${data.aws_caller_identity.current.account_id}
        - ${data.aws_caller_identity.third_party.account_id}
      authorized_session_tag_value_list: 
        - Amazon EMR
      allow_full_table_external_data_access: true
```

## Change Cross Account Version

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      parameters: 
```
