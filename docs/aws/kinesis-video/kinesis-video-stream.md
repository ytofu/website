# Kinesis Video Stream

Manage Kinesis Video Stream resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kinesis_video_stream:
    default:
      name: terraform-kinesis-video-stream
      data_retention_in_hours: 1
      device_name: kinesis-video-device-name
      media_type: video/h264
      tags:
        Name: terraform-kinesis-video-stream
```
