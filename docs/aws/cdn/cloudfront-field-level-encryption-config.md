# Cloudfront Field Level Encryption Config

Manage Cloudfront Field Level Encryption Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_field_level_encryption_config:
    test:
      comment: test comment
      content_type_profile_config:
        forward_when_content_type_is_unknown: true
        content_type_profiles:
          items:
            content_type: application/x-www-form-urlencoded
            format: URLEncoded
      query_arg_profile_config:
        forward_when_query_arg_profile_is_unknown: true
        query_arg_profiles:
          items:
            profile_id: ${aws_cloudfront_field_level_encryption_profile.test.id}
            query_arg: Arg1
```
