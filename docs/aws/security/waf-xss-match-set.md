# Resource: aws_waf_xss_match_set

Provides a WAF XSS Match Set Resource

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

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The name or description of the SizeConstraintSet.
* `xss_match_tuples` - (Optional) The parts of web requests that you want to inspect for cross-site scripting attacks.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF XssMatchSet.
* `arn` - Amazon Resource Name (ARN)

## Import

```bash
ytofu import aws_waf_xss_match_set.example a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
