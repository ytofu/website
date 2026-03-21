# ECS Tag

Manage ECS Tag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_batch_compute_environment:
    example:
      name: example
      service_role: ${aws_iam_role.example.arn}
      type: UNMANAGED

resource:
  aws_ecs_tag:
    example:
      resource_arn: ${aws_batch_compute_environment.example.ecs_cluster_arn}
      key: Name
      value: Hello World
```
