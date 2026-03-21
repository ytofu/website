# Resource: aws_config_configuration_recorder

Provides an AWS Config Configuration Recorder. Please note that this resource **does not start** the created recorder automatically.

## Basic Example

```yaml
resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}

  aws_iam_role:
    r:
      name: awsconfig-example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - config.amazonaws.com
        actions: 
          - "sts:AssumeRole"```

## Exclude Resources Types Usage

```yaml
resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}
      recording_group:
        all_supported: false
        exclusion_by_resource_types:
          resource_types: 
            - "AWS::EC2::Instance"
        recording_strategy:
          use_only: EXCLUSION_BY_RESOURCE_TYPES
```

## Periodic Recording

```yaml
resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}
      recording_group:
        all_supported: false
        include_global_resource_types: false
        resource_types: 
          - "AWS::EC2::Instance"
          - "AWS::EC2::NetworkInterface"
      recording_mode:
        recording_frequency: CONTINUOUS
        recording_mode_override:
          description: Only record EC2 network interfaces daily
          resource_types: 
            - "AWS::EC2::NetworkInterface"
          recording_frequency: DAILY
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional) The name of the recorder. Defaults to `default`. Changing it recreates the resource.
* `role_arn` - (Required) Amazon Resource Name (ARN) of the IAM role. Used to make read or write requests to the delivery channel and to describe the AWS resources associated with the account. See [AWS Docs](http://docs.aws.amazon.com/config/latest/developerguide/iamrole-permissions.html) for more details.
* `recording_group` - (Optional) Recording group - see below.
* `recording_mode` - (Optional) Recording mode - see below.

### recording_group Configuration Block

* `all_supported` - (Optional) Specifies whether AWS Config records configuration changes for every supported type of regional resource (which includes any new type that will become supported in the future). Conflicts with `resource_types`. Defaults to `true`.
* `exclusion_by_resource_types` - (Optional) An object that specifies how AWS Config excludes resource types from being recorded by the configuration recorder.To use this option, you must set the useOnly field of RecordingStrategy to `EXCLUSION_BY_RESOURCE_TYPES` Requires `all_supported = false`. Conflicts with `resource_types`.
* `include_global_resource_types` - (Optional) Specifies whether AWS Config includes all supported types of _global resources_ with the resources that it records. Requires `all_supported = true`. Conflicts with `resource_types`.
* `recording_strategy` - (Optional) Recording Strategy. Detailed below.
* `resource_types` - (Optional) A list that specifies the types of AWS resources for which AWS Config records configuration changes (for example, `AWS::EC2::Instance` or `AWS::CloudTrail::Trail`). See [relevant part of AWS Docs](http://docs.aws.amazon.com/config/latest/APIReference/API_ResourceIdentifier.html#config-Type-ResourceIdentifier-resourceType) for available types. In order to use this attribute, `all_supported` must be set to false.

#### exclusion_by_resource_types Configuration Block

* `resource_types` - (Optional) A list that specifies the types of AWS resources for which AWS Config excludes records configuration changes. See [relevant part of AWS Docs](http://docs.aws.amazon.com/config/latest/APIReference/API_ResourceIdentifier.html#config-Type-ResourceIdentifier-resourceType) for available types.

#### recording_strategy Configuration Block

* ` use_only` - (Optional) The recording strategy for the configuration recorder. See [relevant part of AWS Docs](https://docs.aws.amazon.com/config/latest/APIReference/API_RecordingStrategy.html)

### recording_mode Configuration Block

* `recording_frequency` - (Required) Default recording frequency. `CONTINUOUS` or `DAILY`.
* `recording_mode_override` - (Optional) Recording mode overrides. Detailed below.

#### recording_mode_override Configuration Block

* `description` - (Optional) A description you provide of the override.
* `resource_types` - (Required) A list that specifies the types of AWS resources for which the override applies to.  See [restrictions in the AWS Docs](https://docs.aws.amazon.com/config/latest/APIReference/API_RecordingModeOverride.html)
* `recording_frequency` - (Required) The recording frequency for the resources in the override block. `CONTINUOUS` or `DAILY`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Name of the recorder

## Import

```bash
ytofu import aws_config_configuration_recorder.foo example
```
