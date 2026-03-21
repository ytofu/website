# Lightsail Bucket Resource Access

Manage Lightsail Bucket Resource Access resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_bucket:
    example:
      name: example-bucket
      bundle_id: small_1_0

resource:
  aws_lightsail_instance:
    example:
      name: example-instance
      availability_zone: us-east-1b
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0

resource:
  aws_lightsail_bucket_resource_access:
    example:
      bucket_name: ${aws_lightsail_bucket.example.id}
      resource_name: ${aws_lightsail_instance.example.id}
```
