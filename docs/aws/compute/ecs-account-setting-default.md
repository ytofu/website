# ECS Account Setting Default

Manage ECS Account Setting Default resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecs_account_setting_default:
    test:
      name: taskLongArnFormat
      value: enabled
```

## Set the default log driver mode to non-blocking

```yaml
resource:
  aws_ecs_account_setting_default:
    test:
      name: defaultLogDriverMode
      value: non-blocking
```
