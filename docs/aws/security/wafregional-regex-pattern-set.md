# Resource: aws_wafregional_regex_pattern_set

Provides a WAF Regional Regex Pattern Set Resource

## Basic Example

```yaml
resource:
  aws_wafregional_regex_pattern_set:
    example:
      name: example
      regex_pattern_strings: 
        - one
        - two
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name or description of the Regex Pattern Set.
* `regex_pattern_strings` - (Optional) A list of regular expression (regex) patterns that you want AWS WAF to search for, such as `B[a@]dB[o0]t`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF Regional Regex Pattern Set.

## Import

```bash
ytofu import aws_wafregional_regex_pattern_set.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
