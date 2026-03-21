# Wafregional Sql Injection Match Set

Manage Wafregional Sql Injection Match Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_wafregional_sql_injection_match_set:
    sql_injection_match_set:
      name: tf-sql_injection_match_set
      sql_injection_match_tuple:
        text_transformation: URL_DECODE
        field_to_match:
          type: QUERY_STRING
```
