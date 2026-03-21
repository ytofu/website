# RDS Option Group

Configure database option groups using ytofu YAML.

## SQL Server Option Group

```yaml
resource:
  aws_db_option_group:
    example:
      name: option-group-test
      option_group_description: Terraform Option Group
      engine_name: sqlserver-ee
      major_engine_version: "11.00"
      option:
        - option_name: Timezone
          option_settings:
            - name: TIME_ZONE
              value: UTC
        - option_name: SQLSERVER_BACKUP_RESTORE
          option_settings:
            - name: IAM_ROLE_ARN
              value: ${aws_iam_role.example.arn}
```
