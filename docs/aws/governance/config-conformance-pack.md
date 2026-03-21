# Config Conformance Pack

Manage Config Conformance Pack resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_config_conformance_pack:
    example:
      name: example
      input_parameter:
        parameter_name: AccessKeysRotatedParameterMaxAccessKeyAge
        parameter_value: 90
      template_body: |
        Parameters:
        AccessKeysRotatedParameterMaxAccessKeyAge:
        Type: String
        Resources:
        IAMPasswordPolicy:
        Properties:
        ConfigRuleName: IAMPasswordPolicy
        Source:
        Owner: AWS
        SourceIdentifier: IAM_PASSWORD_POLICY
        Type: AWS::Config::ConfigRule
      depends_on: 
        - ${aws_config_configuration_recorder.example}
```

## Template S3 URI

```yaml
resource:
  aws_config_conformance_pack:
    example:
      name: example
      template_s3_uri: "s3://${aws_s3_bucket.example.bucket}/${aws_s3_object.example.key}"
      depends_on: 
        - ${aws_config_configuration_recorder.example}

resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.example.id}
      key: example-key
      content: |
        Resources:
        IAMPasswordPolicy:
        Properties:
        ConfigRuleName: IAMPasswordPolicy
        Source:
        Owner: AWS
        SourceIdentifier: IAM_PASSWORD_POLICY
        Type: AWS::Config::ConfigRule
```
