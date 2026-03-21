# IVS Recording Configuration

Manage IVS Recording Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ivs_recording_configuration:
    example:
      name: recording_configuration-1
      destination_configuration:
        s3:
          bucket_name: ivs-stream-archive
```
