# AWS Config Recorder

Configure AWS Config recording using ytofu YAML.

## Basic Recorder

```yaml
resource:
  aws_config_configuration_recorder:
    example:
      name: example
      role_arn: ${aws_iam_role.config.arn}

  aws_config_configuration_recorder_status:
    example:
      name: ${aws_config_configuration_recorder.example.name}
      is_enabled: true
      depends_on:
        - aws_config_delivery_channel.example
```

## Record All Resources

```yaml
resource:
  aws_config_configuration_recorder:
    example:
      name: example
      role_arn: ${aws_iam_role.config.arn}
      recording_group:
        all_supported: true
        include_global_resource_types: true
```

## Record Specific Resources

```yaml
resource:
  aws_config_configuration_recorder:
    example:
      name: example
      role_arn: ${aws_iam_role.config.arn}
      recording_group:
        all_supported: false
        resource_types:
          - AWS::EC2::Instance
          - AWS::S3::Bucket
          - AWS::IAM::Role
```
