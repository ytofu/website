# Resource: aws_config_conformance_pack

Manages a Config Conformance Pack. More information about this collection of Config rules and remediation actions can be found in the
[Conformance Packs](https://docs.aws.amazon.com/config/latest/developerguide/conformance-packs.html) documentation.
Sample Conformance Pack templates may be found in the
[AWS Config Rules Repository](https://github.com/awslabs/aws-config-rules/tree/master/aws-config-conformance-packs).

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

  aws_s3_bucket:
    example:
      bucket: example

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
        Type: AWS::Config::ConfigRule```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required, Forces new resource) The name of the conformance pack. Must begin with a letter and contain from 1 to 256 alphanumeric characters and hyphens.
* `delivery_s3_bucket` - (Optional) Amazon S3 bucket where AWS Config stores conformance pack templates. Maximum length of 63.
* `delivery_s3_key_prefix` - (Optional) The prefix for the Amazon S3 bucket. Maximum length of 1024.
* `input_parameter` - (Optional) Set of configuration blocks describing input parameters passed to the conformance pack template. Documented below. When configured, the parameters must also be included in the `template_body` or in the template stored in Amazon S3 if using `template_s3_uri`.
* `template_body` - (Optional, required if `template_s3_uri` is not provided) A string containing full conformance pack template body. Maximum length of 51200. Drift detection is not possible with this argument.
* `template_s3_uri` - (Optional, required if `template_body` is not provided) Location of file, e.g., `s3://bucketname/prefix`, containing the template body. The uri must point to the conformance pack template that is located in an Amazon S3 bucket in the same region as the conformance pack. Maximum length of 1024. Drift detection is not possible with this argument.

### input_parameter Argument Reference

The `input_parameter` configuration block supports the following arguments:

* `parameter_name` - (Required) The input key.
* `parameter_value` - (Required) The input value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the conformance pack.

## Import

```bash
ytofu import aws_config_conformance_pack.example example
```
