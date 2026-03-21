# Resource: aws_waf_geo_match_set

Provides a WAF Geo Match Set Resource

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

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The name or description of the GeoMatchSet.
* `geo_match_constraint` - (Optional) The GeoMatchConstraint objects which contain the country that you want AWS WAF to search for.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF GeoMatchSet.
* `arn` - Amazon Resource Name (ARN)

## Import

```bash
ytofu import aws_waf_geo_match_set.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
