# Bedrock Model Invocation Logging

Configure invocation logging for Bedrock using ytofu YAML.

## S3 Logging

```yaml
resource:
  aws_bedrock_model_invocation_logging_configuration:
    example:
      logging_config:
        embedding_data_delivery_enabled: true
        text_data_delivery_enabled: true
        image_data_delivery_enabled: true
        s3_config:
          bucket_name: ${aws_s3_bucket.bedrock_logs.id}
          key_prefix: bedrock/
```

## CloudWatch Logging

```yaml
resource:
  aws_bedrock_model_invocation_logging_configuration:
    example:
      logging_config:
        text_data_delivery_enabled: true
        cloudwatch_config:
          log_group_name: /aws/bedrock/invocations
          role_arn: ${aws_iam_role.bedrock_logging.arn}
```
