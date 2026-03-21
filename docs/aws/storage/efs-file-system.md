# EFS File System

Manage EFS File System resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_efs_file_system:
    foo:
      creation_token: my-product
      tags:
        Name: MyProduct
```

## Using lifecycle policy

```yaml
resource:
  aws_efs_file_system:
    foo_with_lifecyle_policy:
      creation_token: my-product
      lifecycle_policy:
        transition_to_ia: AFTER_30_DAYS
```
