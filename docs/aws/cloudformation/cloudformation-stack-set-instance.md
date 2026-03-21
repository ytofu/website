# Resource: aws_cloudformation_stack_set_instance

Manages a CloudFormation StackSet Instance. Instances are managed in the account and region of the StackSet after the target account permissions have been configured. Additional information about StackSets can be found in the [AWS CloudFormation User Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/what-is-cfnstacksets.html).

## Basic Example

```yaml
resource:
  aws_cloudformation_stack_set_instance:
    example:
      account_id: 123456789012
      stack_set_instance_region: us-east-1
      stack_set_name: ${aws_cloudformation_stack_set.example.name}
```

## Example IAM Setup in Target Account

```yaml
data:
  aws_iam_policy_document:
    AWSCloudFormationStackSetExecutionRole_assume_role_policy:
      statement:
        actions: 
          - "sts:AssumeRole"
        effect: Allow
        principals:
          identifiers: 
            - ${aws_iam_role.AWSCloudFormationStackSetAdministrationRole.arn}
          type: AWS

  aws_iam_policy_document:
    AWSCloudFormationStackSetExecutionRole_MinimumExecutionPolicy:
      statement:
        actions:
          - "cloudformation:*"
          - "s3:*"
          - "sns:*"
        effect: Allow
        resources: 
          - "*"

resource:
  aws_iam_role:
    AWSCloudFormationStackSetExecutionRole:
      assume_role_policy: ${data.aws_iam_policy_document.AWSCloudFormationStackSetExecutionRole_assume_role_policy.json}
      name: AWSCloudFormationStackSetExecutionRole

  aws_iam_role_policy:
    AWSCloudFormationStackSetExecutionRole_MinimumExecutionPolicy:
      name: MinimumExecutionPolicy
      policy: ${data.aws_iam_policy_document.AWSCloudFormationStackSetExecutionRole_MinimumExecutionPolicy.json}
      role: ${aws_iam_role.AWSCloudFormationStackSetExecutionRole.name}```

## Example Deployment across Organizations account

```yaml
resource:
  aws_cloudformation_stack_set_instance:
    example:
      deployment_targets:
        organizational_unit_ids: 
          - ${aws_organizations_organization.example.roots[0].id}
      stack_set_instance_region: us-east-1
      stack_set_name: ${aws_cloudformation_stack_set.example.name}
```

## Argument Reference

This resource supports the following arguments:

* `stack_set_name` - (Required) Name of the StackSet.
* `account_id` - (Optional) Target AWS Account ID to create a Stack based on the StackSet. Defaults to current account.
* `call_as` - (Optional) Specifies whether you are acting as an account administrator in the organization's management account or as a delegated administrator in a member account. Valid values: `SELF` (default), `DELEGATED_ADMIN`.
* `deployment_targets` - (Optional) AWS Organizations accounts to which StackSets deploys. StackSets doesn't deploy stack instances to the organization management account, even if the organization management account is in your organization or in an OU in your organization. Drift detection is not possible for this argument. See [deployment_targets](#deployment_targets-argument-reference) below.
* `operation_preferences` - (Optional) Preferences for how AWS CloudFormation performs a stack set operation.
* `parameter_overrides` - (Optional) Key-value map of input parameters to override from the StackSet for this Instance.
* `retain_stack` - (Optional) During ytofu resource destroy, remove Instance from StackSet while keeping the Stack and its associated resources. Must be enabled in ytofu state _before_ destroy operation to take effect. You cannot reassociate a retained Stack or add an existing, saved Stack to a new StackSet. Defaults to `false`.
* `stack_set_instance_region` - Target AWS Region to create a Stack based on the StackSet. Defaults to current region.

### `deployment_targets` Argument Reference

The `deployment_targets` configuration block supports the following arguments:

* `organizational_unit_ids` - (Optional) Organization root ID or organizational unit (OU) IDs to which StackSets deploys.
* `account_filter_type` - (Optional) Limit deployment targets to individual accounts or include additional accounts with provided OUs. Valid values: `INTERSECTION`, `DIFFERENCE`, `UNION`, `NONE`.
* `accounts` - (Optional) List of accounts to deploy stack set updates.
* `accounts_url` - (Optional) S3 URL of the file containing the list of accounts.

### `operation_preferences` Argument Reference

The `operation_preferences` configuration block supports the following arguments:

* `failure_tolerance_count` - (Optional) Number of accounts, per Region, for which this operation can fail before AWS CloudFormation stops the operation in that Region.
* `failure_tolerance_percentage` - (Optional) Percentage of accounts, per Region, for which this stack operation can fail before AWS CloudFormation stops the operation in that Region.
* `max_concurrent_count` - (Optional) Maximum number of accounts in which to perform this operation at one time.
* `max_concurrent_percentage` - (Optional) Maximum percentage of accounts in which to perform this operation at one time.
* `concurrency_mode` - (Optional) Specifies how the concurrency level behaves during the operation execution. Valid values are `STRICT_FAILURE_TOLERANCE` and `SOFT_FAILURE_TOLERANCE`.
* `region_concurrency_type` - (Optional) Concurrency type of deploying StackSets operations in Regions, could be in parallel or one Region at a time. Valid values are `SEQUENTIAL` and `PARALLEL`.
* `region_order` - (Optional) Order of the Regions in where you want to perform the stack operation.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Unique identifier for the resource. If `deployment_targets` is set, this is a comma-delimited string combining stack set name, organizational unit IDs (`/`-delimited), and region (ie. `mystack,ou-123/ou-456,us-east-1`). Otherwise, this is a comma-delimited string combining stack set name, AWS account ID, and region (ie. `mystack,123456789012,us-east-1`).
* `organizational_unit_id` - Organization root ID or organizational unit (OU) ID in which the stack is deployed.
* `stack_id` - Stack identifier.
* `stack_instance_summaries` - List of stack instances created from an organizational unit deployment target. This will only be populated when `deployment_targets` is set. See [`stack_instance_summaries`](#stack_instance_summaries-attribute-reference).

### `stack_instance_summaries` Attribute Reference

* `account_id` - AWS account ID in which the stack is deployed.
* `organizational_unit_id` - Organizational unit ID in which the stack is deployed.
* `stack_id` - Stack identifier.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_cloudformation_stack_set_instance.example example,123456789012,us-east-1
```
