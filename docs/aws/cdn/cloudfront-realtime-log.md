# CloudFront Realtime Log Config

Configure realtime logging for CloudFront using ytofu YAML.

## Basic Realtime Log

```yaml
resource:
  aws_cloudfront_realtime_log_config:
    example:
      name: example
      sampling_rate: 75
      fields:
        - timestamp
        - c-ip
        - sc-status
        - cs-uri-stem
      endpoint:
        stream_type: Kinesis
        kinesis_stream_config:
          role_arn: ${aws_iam_role.example.arn}
          stream_arn: ${aws_kinesis_stream.example.arn}
```
