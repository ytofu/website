# Glue User Defined Function

Manage Glue User Defined Function resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_catalog_database:
    example:
      name: my_database

resource:
  aws_glue_user_defined_function:
    example:
      name: my_func
      catalog_id: ${aws_glue_catalog_database.example.catalog_id}
      database_name: ${aws_glue_catalog_database.example.name}
      class_name: class
      owner_name: owner
      owner_type: GROUP
      resource_uris:
        resource_type: ARCHIVE
        uri: uri
```
