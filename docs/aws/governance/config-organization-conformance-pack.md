# Resource: aws_config_organization_conformance_pack

Manages a Config Organization Conformance Pack. More information can be found in the [Managing Conformance Packs Across all Accounts in Your Organization](https://docs.aws.amazon.com/config/latest/developerguide/conformance-pack-organization-apis.html) and [AWS Config Managed Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_use-managed-rules.html) documentation. Example conformance pack templates may be found in the [AWS Config Rules Repository](https://github.com/awslabs/aws-config-rules/tree/master/aws-config-conformance-packs).

## Basic Example

```yaml
resource:
  aws_config_organization_conformance_pack:
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
        - ${aws_organizations_organization.example}

  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - config-multiaccountsetup.amazonaws.com
      feature_set: ALL```

## Using Template S3 URI

```yaml
resource:
  aws_config_organization_conformance_pack:
    example:
      name: example
      template_s3_uri: "s3://${aws_s3_bucket.example.bucket}/${aws_s3_object.example.key}"
      depends_on: 
        - ${aws_config_configuration_recorder.example}
        - ${aws_organizations_organization.example}

  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - config-multiaccountsetup.amazonaws.com
      feature_set: ALL

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
* `name` - (Required, Forces new resource) The name of the organization conformance pack. Must begin with a letter and contain from 1 to 128 alphanumeric characters and hyphens.
* `delivery_s3_bucket` - (Optional) Amazon S3 bucket where AWS Config stores conformance pack templates. Delivery bucket must begin with `awsconfigconforms` prefix. Maximum length of 63.
* `delivery_s3_key_prefix` - (Optional) The prefix for the Amazon S3 bucket. Maximum length of 1024.
* `excluded_accounts` - (Optional) Set of AWS accounts to be excluded from an organization conformance pack while deploying a conformance pack. Maximum of 1000 accounts.
* `input_parameter` - (Optional) Set of configuration blocks describing input parameters passed to the conformance pack template. Documented below. When configured, the parameters must also be included in the `template_body` or in the template stored in Amazon S3 if using `template_s3_uri`.
* `template_body` - (Optional, Conflicts with `template_s3_uri`) A string containing full conformance pack template body. Maximum length of 51200. Drift detection is not possible with this argument.
* `template_s3_uri` - (Optional, Conflicts with `template_body`) Location of file, e.g., `s3://bucketname/prefix`, containing the template body. The uri must point to the conformance pack template that is located in an Amazon S3 bucket in the same region as the conformance pack. Maximum length of 1024. Drift detection is not possible with this argument.

### input_parameter Argument Reference

The `input_parameter` configuration block supports the following arguments:

* `parameter_name` - (Required) The input key.
* `parameter_value` - (Required) The input value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the organization conformance pack.
* `id` - The name of the organization conformance pack.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `update` - (Default `10m`)
- `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_config_organization_conformance_pack.example example
```
