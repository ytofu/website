# Cleanrooms Configured Table

Manage Cleanrooms Configured Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cleanrooms_configured_table:
    test_configured_table:
      name: terraform-example-table
      description: I made this table with terraform!
      analysis_method: DIRECT_QUERY
      allowed_columns:
        - column1
        - column2
        - column3
      table_reference:
        database_name: example_database
        table_name: example_table
      tags:
        Project: Terraform
```
