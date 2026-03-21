# Resource: aws_wafregional_geo_match_set

Provides a WAF Regional Geo Match Set Resource

## Basic Example

```yaml
resource:
  aws_wafregional_geo_match_set:
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

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name or description of the Geo Match Set.
* `geo_match_constraint` - (Optional) The Geo Match Constraint objects which contain the country that you want AWS WAF to search for.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF Regional Geo Match Set.

## Import

```bash
ytofu import aws_wafregional_geo_match_set.geo_match_set a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
