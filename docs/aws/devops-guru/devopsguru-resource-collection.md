# Devopsguru Resource Collection

Manage Devopsguru Resource Collection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_devopsguru_resource_collection:
    example:
      type: AWS_SERVICE
      cloudformation:
        stack_names: 
          - "*"
```

## CloudFormation Stacks

```yaml
resource:
  aws_devopsguru_resource_collection:
    example:
      type: AWS_CLOUD_FORMATION
      cloudformation:
        stack_names: 
          - ExampleStack
```

## Tags

```yaml
resource:
  aws_devopsguru_resource_collection:
    example:
      type: AWS_TAGS
      tags:
        app_boundary_key: DevOps-Guru-Example
        tag_values: 
          - Example-Value
```

## Tags All Resources

```yaml
resource:
  aws_devopsguru_resource_collection:
    example:
      type: AWS_TAGS
      tags:
        app_boundary_key: DevOps-Guru-Example
        tag_values: 
          - "*"
```
