# Sagemaker Notebook Instance Lifecycle Configuration

Manage Sagemaker Notebook Instance Lifecycle Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_notebook_instance_lifecycle_configuration:
    lc:
      name: foo
      on_create: base64-encoded-content
      on_start: base64-encoded-content
```
