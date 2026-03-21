# S3 Object Copy

Manage S3 Object Copy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_object_copy:
    test:
      bucket: destination_bucket
      key: destination_key
      source: source_bucket/source_key
      grant:
        uri: "http://acs.amazonaws.com/groups/global/AllUsers"
        type: Group
        permissions: 
          - READ
```

## Ignoring Provider `default_tags`

```yaml
resource:
  aws_s3_object_copy:
    test:
      bucket: destination_bucket
      key: destination_key
      source: source_bucket/source_key
      override_provider:
        default_tags:
          tags: {}
```
