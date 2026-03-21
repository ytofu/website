# Lightsail Bucket Access Key

Manage Lightsail Bucket Access Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_bucket:
    example:
      name: example-bucket
      bundle_id: small_1_0

resource:
  aws_lightsail_bucket_access_key:
    example:
      bucket_name: ${aws_lightsail_bucket.example.id}
```
