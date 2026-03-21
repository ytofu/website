# Budgets Budget Action

Manage Budgets Budget Action resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_budgets_budget_action:
    example:
      budget_name: ${aws_budgets_budget.example.name}
      action_type: APPLY_IAM_POLICY
      approval_model: AUTOMATIC
      notification_type: ACTUAL
      execution_role_arn: ${aws_iam_role.example.arn}
      action_threshold:
        action_threshold_type: ABSOLUTE_VALUE
        action_threshold_value: 100
      definition:
        iam_action_definition:
          policy_arn: ${aws_iam_policy.example.arn}
          roles: 
            - ${aws_iam_role.example.name}
      subscriber:
        address: example@example.example
        subscription_type: EMAIL
      tags:
        Tag1: Value1
        Tag2: Value2

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        actions: 
          - "ec2:Describe*"
        resources: 
          - "*"

resource:
  aws_iam_policy:
    example:
      name: example
      description: My example policy
      policy: ${data.aws_iam_policy_document.example.json}

data:
  aws_partition:
    current:

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - "budgets.${data.aws_partition.current.dns_suffix}"
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_budgets_budget:
    example:
      name: example
      budget_type: USAGE
      limit_amount: 10.0
      limit_unit: dollars
      time_period_start: "2006-01-02_15:04"
      time_unit: MONTHLY
```
