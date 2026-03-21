# AWS Config Rule

Create compliance rules using ytofu YAML.

## Managed Rule

```yaml
resource:
  aws_config_config_rule:
    s3_bucket_versioning:
      name: s3-bucket-versioning-enabled
      source:
        owner: AWS
        source_identifier: S3_BUCKET_VERSIONING_ENABLED
      depends_on:
        - aws_config_configuration_recorder.example
```

## With Input Parameters

```yaml
resource:
  aws_config_config_rule:
    instance_type:
      name: desired-instance-type
      source:
        owner: AWS
        source_identifier: DESIRED_INSTANCE_TYPE
      input_parameters: example-json-policy
```

## Custom Rule (Lambda)

```yaml
resource:
  aws_config_config_rule:
    custom:
      name: custom-compliance-check
      source:
        owner: CUSTOM_LAMBDA
        source_identifier: ${aws_lambda_function.config_check.arn}
        source_detail:
          - event_source: aws.config
            message_type: ConfigurationItemChangeNotification
      scope:
        compliance_resource_types:
          - AWS::EC2::Instance
```
