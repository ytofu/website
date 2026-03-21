# Athena Data Catalog

Manage Athena Data Catalog resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: athena-data-catalog
      description: Example Athena data catalog
      type: LAMBDA
      parameters: 
      tags:
        Name: example-athena-data-catalog
```

## Hive based Data Catalog

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: hive-data-catalog
      description: Hive based Data Catalog
      type: HIVE
      parameters: 
```

## Glue based Data Catalog

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: glue-data-catalog
      description: Glue based Data Catalog
      type: GLUE
      parameters: 
```

## Lambda based Data Catalog

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: lambda-data-catalog
      description: Lambda based Data Catalog
      type: LAMBDA
      parameters: 
```
