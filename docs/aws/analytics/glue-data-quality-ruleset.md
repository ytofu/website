# Glue Data Quality Ruleset

Manage Glue Data Quality Ruleset resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
```

## With description

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      description: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
```

## With tags

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
      tags: 
```

## With target_table

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
      target_table:
        database_name: ${aws_glue_catalog_database.example.name}
        table_name: ${aws_glue_catalog_table.example.name}
```
