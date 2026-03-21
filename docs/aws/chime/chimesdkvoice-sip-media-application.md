# Chimesdkvoice Sip Media Application

Manage Chimesdkvoice Sip Media Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_chimesdkvoice_sip_media_application:
    example:
      aws_region: us-east-1
      name: example-sip-media-application
      endpoints:
        lambda_arn: ${aws_lambda_function.test.arn}
```
