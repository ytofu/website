# Ssmquicksetup Configuration Manager

Manage Ssmquicksetup Configuration Manager resources using ytofu YAML.

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
