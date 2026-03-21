# Cloudformation Stack Set Instance

Manage Cloudformation Stack Set Instance resources using ytofu YAML.

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

resource:
  aws_iam_role:
    AWSCloudFormationStackSetExecutionRole:
      assume_role_policy: ${data.aws_iam_policy_document.AWSCloudFormationStackSetExecutionRole_assume_role_policy.json}
      name: AWSCloudFormationStackSetExecutionRole

data:
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
  aws_iam_role_policy:
    AWSCloudFormationStackSetExecutionRole_MinimumExecutionPolicy:
      name: MinimumExecutionPolicy
      policy: ${data.aws_iam_policy_document.AWSCloudFormationStackSetExecutionRole_MinimumExecutionPolicy.json}
      role: ${aws_iam_role.AWSCloudFormationStackSetExecutionRole.name}
```

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
