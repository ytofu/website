# Lakeformation Data Cells Filter

Manage Lakeformation Data Cells Filter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lakeformation_data_cells_filter:
    example:
      table_data:
        database_name: ${aws_glue_catalog_database.example.name}
        name: example
        table_catalog_id: ${data.aws_caller_identity.current.account_id}
        table_name: ${aws_glue_catalog_table.example.name}
        column_names: 
          - my_column
        row_filter:
          filter_expression: "my_column='example'"
```

## Filter with Excluded Columns Only (No Row Filter)

```yaml
resource:
  aws_lakeformation_data_cells_filter:
    excluded_columns:
      table_data:
        database_name: ${aws_glue_catalog_database.example.name}
        name: exclude-pii
        table_catalog_id: ${data.aws_caller_identity.current.account_id}
        table_name: ${aws_glue_catalog_table.example.name}
        column_wildcard:
          excluded_column_names: 
            - ssn
            - credit_card
        row_filter:
          all_rows_wildcard:
```

## Filter with Row Filter and Excluded Columns

```yaml
resource:
  aws_lakeformation_data_cells_filter:
    row_and_column:
      table_data:
        database_name: ${aws_glue_catalog_database.example.name}
        name: marketing-filtered
        table_catalog_id: ${data.aws_caller_identity.current.account_id}
        table_name: ${aws_glue_catalog_table.example.name}
        column_wildcard:
          excluded_column_names: 
            - salary
            - bonus
        row_filter:
          filter_expression: "department = 'Marketing'"
```

## Filter with Row Filter Only (All Columns Included)

```yaml
resource:
  aws_lakeformation_data_cells_filter:
    row_only:
      table_data:
        database_name: ${aws_glue_catalog_database.example.name}
        name: regional-filter
        table_catalog_id: ${data.aws_caller_identity.current.account_id}
        table_name: ${aws_glue_catalog_table.example.name}
        column_wildcard:
          excluded_column_names: []
        row_filter:
          filter_expression: "region = 'US-WEST'"
```
