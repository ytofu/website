# WAF Sql Injection Match Set

Manage WAF Sql Injection Match Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_waf_sql_injection_match_set:
    sql_injection_match_set:
      name: tf-sql_injection_match_set
      sql_injection_match_tuples:
        text_transformation: URL_DECODE
        field_to_match:
          type: QUERY_STRING
```
