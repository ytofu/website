# Ssoadmin Application Assignment

Manage Ssoadmin Application Assignment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssoadmin_application_assignment:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      principal_id: ${aws_identitystore_user.example.user_id}
      principal_type: USER
```

## Group Type

```yaml
resource:
  aws_ssoadmin_application_assignment:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      principal_id: ${aws_identitystore_group.example.group_id}
      principal_type: GROUP
```
