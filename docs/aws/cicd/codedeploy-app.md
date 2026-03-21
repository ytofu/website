# Codedeploy App

Manage Codedeploy App resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codedeploy_app:
    example:
      compute_platform: ECS
      name: example
```

## Lambda Application

```yaml
resource:
  aws_codedeploy_app:
    example:
      compute_platform: Lambda
      name: example
```

## Server Application

```yaml
resource:
  aws_codedeploy_app:
    example:
      compute_platform: Server
      name: example
```
