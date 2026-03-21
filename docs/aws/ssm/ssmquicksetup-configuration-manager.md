# Resource: aws_ssmquicksetup_configuration_manager

ytofu resource for managing an AWS SSM Quick Setup Configuration Manager.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

data:
  aws_region:
    current:

data:
  aws_ssm_patch_baselines:
    example:
      default_baselines: true

resource:
  aws_ssmquicksetup_configuration_manager:
    example:
      name: example
      configuration_definition:
        local_deployment_administration_role_arn: "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:role/AWS-QuickSetup-PatchPolicy-LocalAdministrationRole"
        local_deployment_execution_role_name: AWS-QuickSetup-PatchPolicy-LocalExecutionRole
        type: AWSQuickSetupType-PatchPolicy
        parameters: 
```

## Argument Reference

The following arguments are required:

* `configuration_definition` - (Required) Definition of the Quick Setup configuration that the configuration manager deploys. See [`configuration_definition`](#configuration_definition-argument-reference) below.
* `name` - (Required) Configuration manager name.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the configuration manager.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### `configuration_definition` Argument Reference

* `local_deployment_administrator_role_arn` - (Optional) ARN of the IAM role used to administrate local configuration deployments.
* `local_deployment_execution_role_name` - (Optional) Name of the IAM role used to deploy local configurations.
* `parameters` - (Required) Parameters for the configuration definition type. Parameters for configuration definitions vary based the configuration type. See the [AWS API documentation](https://docs.aws.amazon.com/quick-setup/latest/APIReference/API_ConfigurationDefinitionInput.html) for a complete list of parameters for each configuration type.
* `type` - (Required) Type of the Quick Setup configuration.
* `type_version` - (Optional) Version of the Quick Setup type to use.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `manager_arn` - ARN of the Configuration Manager.
* `status_summaries` - A summary of the state of the configuration manager. This includes deployment statuses, association statuses, drift statuses, health checks, and more. See [`status_summaries`](#status_summaries-attribute-reference) below.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

### `status_summaries` Attribute Reference

* `status` - Current status.
* `status_message` - When applicable, returns an informational message relevant to the current status and status type of the status summary object.
* `status_type` - Type of a status summary.

## Timeouts

Configuration options:

* `create` - (Default `20m`)
* `update` - (Default `20m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_ssmquicksetup_configuration_manager.example arn:aws:ssm-quicksetup:us-east-1:012345678901:configuration-manager/abcd-1234
```
