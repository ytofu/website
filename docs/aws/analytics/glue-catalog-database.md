# Glue Catalog Database

Manage Glue Catalog Database resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_catalog_database:
    example:
      name: MyCatalogDatabase
```

## Create Table Default Permissions

```yaml
resource:
  aws_glue_catalog_database:
    example:
      name: MyCatalogDatabase
      create_table_default_permission:
        permissions: 
          - SELECT
        principal:
          data_lake_principal_identifier: IAM_ALLOWED_PRINCIPALS
```
