# Resource: aws_lakeformation_data_cells_filter

ytofu resource for managing an AWS Lake Formation Data Cells Filter.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `table_data` - (Required) Information about the data cells filter. See [Table Data](#table-data) below for details.

### Table Data

* `database_name` - (Required) The name of the database.
* `name` - (Required) The name of the data cells filter.
* `table_catalog_id` - (Required) The ID of the Data Catalog.
* `table_name` - (Required) The name of the table.
* `column_names` - (Optional) A list of column names and/or nested column attributes.
* `column_wildcard` - (Optional) A wildcard with exclusions. See [Column Wildcard](#column-wildcard) below for details.
* `row_filter` - (Optional) A PartiQL predicate. See [Row Filter](#row-filter) below for details.
* `version_id` - (Optional) ID of the data cells filter version.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Provider composed identifier: `database_name,name,table_catalog_id,table_name`.

#### Column Wildcard

* `excluded_column_names` - (Optional) Excludes column names. Any column with this name will be excluded.

#### Row Filter

**Note:** Exactly one of `filter_expression` or `all_rows_wildcard` must be specified.

* `all_rows_wildcard` - (Optional) A wildcard that matches all rows. Required when applying column-level filtering without row-level filtering. Use an empty block: `all_rows_wildcard {}`.
* `filter_expression` - (Optional) A PartiQL predicate expression for row-level filtering.

## Timeouts

Configuration options:

- `create` - (Default `2m`)

## Import

```bash
ytofu import aws_lakeformation_data_cells_filter.example database_name,name,table_catalog_id,table_name
```
