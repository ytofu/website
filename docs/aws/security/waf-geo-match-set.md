# WAF Geo Match Set

Manage WAF Geo Match Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_waf_geo_match_set:
    geo_match_set:
      name: geo_match_set
      geo_match_constraint:
        type: Country
        value: US
      geo_match_constraint:
        type: Country
        value: CA
```
