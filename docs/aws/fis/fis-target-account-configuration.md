# FIS Target Account Configuration

Manage FIS Target Account Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fis_target_account_configuration:
    example:
      experiment_template_id: ${aws_fis_experiment_template.example.id}
      account_id: ${data.aws_caller_identity.current.account_id}
      role_arn: ${aws_iam_role.fis_role.arn}
      description: Example
```
