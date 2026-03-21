# Resource: aws_waf_regex_pattern_set

Provides a WAF Regex Pattern Set Resource

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

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The name or description of the Regex Pattern Set.
* `regex_pattern_strings` - (Optional) A list of regular expression (regex) patterns that you want AWS WAF to search for, such as `B[a@]dB[o0]t`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF Regex Pattern Set.
* `arn` - Amazon Resource Name (ARN)

## Import

```bash
ytofu import aws_waf_regex_pattern_set.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
