# ECS Express Gateway Service

Manage ECS Express Gateway Service resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecs_express_gateway_service:
    example:
      execution_role_arn: ${aws_iam_role.execution.arn}
      infrastructure_role_arn: ${aws_iam_role.infrastructure.arn}
      primary_container:
        image: "nginx:latest"
```
