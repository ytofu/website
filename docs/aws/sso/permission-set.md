# SSO Permission Set

Create permission sets for IAM Identity Center using ytofu YAML.

## Basic Permission Set

```yaml
data:
  aws_ssoadmin_instances:
    example: {}

resource:
  aws_ssoadmin_permission_set:
    example:
      name: AdminAccess
      description: Admin access permission set
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      session_duration: PT8H
      tags:
        ManagedBy: tofu
```

## With Relay State

```yaml
resource:
  aws_ssoadmin_permission_set:
    example:
      name: ConsoleAccess
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      relay_state: https://console.aws.amazon.com/
```
