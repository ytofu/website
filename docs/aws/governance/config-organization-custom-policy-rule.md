# Resource: aws_config_organization_custom_policy_rule

Manages a Config Organization Custom Policy Rule. More information about these rules can be found in the [Enabling AWS Config Rules Across all Accounts in Your Organization](https://docs.aws.amazon.com/config/latest/developerguide/config-rule-multi-account-deployment.html) and [AWS Config Managed Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_use-managed-rules.html) documentation. For working with Organization Managed Rules (those invoking an AWS managed rule), see the `aws_config_organization_managed__rule` resource.

## Basic Example

```yaml
resource:
  aws_config_organization_custom_policy_rule:
    example:
      name: example_rule_name
      policy_runtime: guard-2.x.x
      policy_text: |
        let status = ['ACTIVE']
        
        rule tableisactive when
        resourceType == "AWS::DynamoDB::Table" {
        configuration.tableStatus == %status
        }
        
        rule checkcompliance when
        resourceType == "AWS::DynamoDB::Table"
        tableisactive {
        let pitr = supplementaryConfiguration.ContinuousBackupsDescription.pointInTimeRecoveryDescription.pointInTimeRecoveryStatus
        %pitr == "ENABLED"
        }
      resource_types_scope: 
        - "AWS::DynamoDB::Table"
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the rule.
* `policy_text` - (Required) Policy definition containing the rule logic.
* `policy_runtime` - (Required)  Runtime system for policy rules.
* `trigger_types` - (Required) List of notification types that trigger AWS Config to run an evaluation for the rule. Valid values: `ConfigurationItemChangeNotification`, `OversizedConfigurationItemChangeNotification`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the rule.
* `debug_log_delivery_accounts` - (Optional) List of accounts that you can enable debug logging for. The list is null when debug logging is enabled for all accounts.
* `excluded_accounts` - (Optional) List of AWS account identifiers to exclude from the rule.
* `input_parameters` - (Optional) A string in JSON format that is passed to the AWS Config Rule Lambda Function.
* `maximum_execution_frequency` - (Optional) Maximum frequency with which AWS Config runs evaluations for a rule, if the rule is triggered at a periodic frequency. Defaults to `TwentyFour_Hours` for periodic frequency triggered rules. Valid values: `One_Hour`, `Three_Hours`, `Six_Hours`, `Twelve_Hours`, or `TwentyFour_Hours`.
* `resource_id_scope` - (Optional) Identifier of the AWS resource to evaluate.
* `resource_types_scope` - (Optional) List of types of AWS resources to evaluate.
* `tag_key_scope` - (Optional, Required if `tag_value_scope` is configured) Tag key of AWS resources to evaluate.
* `tag_value_scope` - (Optional) Tag value of AWS resources to evaluate.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the rule.

## Timeouts

Configuration options:

* `create` - (Default `20m`)
* `update` - (Default `20m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_config_organization_custom_policy_rule.example example_rule_name
```
