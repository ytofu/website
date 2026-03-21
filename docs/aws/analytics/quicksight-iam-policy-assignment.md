# Quicksight IAM Policy Assignment

Manage Quicksight IAM Policy Assignment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_iam_policy_assignment:
    example:
      assignment_name: example
      assignment_status: ENABLED
      policy_arn: ${aws_iam_policy.example.arn}
      identities:
        user: 
          - ${aws_quicksight_user.example.user_name}
```
