# Resource: aws_waf_sql_injection_match_set

Provides a WAF SQL Injection Match Set Resource

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

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The name or description of the SQL Injection Match Set.
* `sql_injection_match_tuples` - (Optional) The parts of web requests that you want AWS WAF to inspect for malicious SQL code and, if you want AWS WAF to inspect a header, the name of the header.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF SQL Injection Match Set.
* `arn` - Amazon Resource Name (ARN) of the SQL injection match set.

## Import

```bash
ytofu import aws_waf_sql_injection_match_set.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
