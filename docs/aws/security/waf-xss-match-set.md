# WAF Xss Match Set

Manage WAF Xss Match Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_waf_xss_match_set:
    xss_match_set:
      name: xss_match_set
      xss_match_tuples:
        text_transformation: NONE
        field_to_match:
          type: URI
      xss_match_tuples:
        text_transformation: NONE
        field_to_match:
          type: QUERY_STRING
```
