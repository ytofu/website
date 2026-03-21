# WAF Regex Pattern Set

Manage WAF Regex Pattern Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_waf_regex_pattern_set:
    example:
      name: tf_waf_regex_pattern_set
      regex_pattern_strings: 
        - one
        - two
```
