# Sagemaker Studio Lifecycle Config

Manage Sagemaker Studio Lifecycle Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_studio_lifecycle_config:
    example:
      studio_lifecycle_config_name: example
      studio_lifecycle_config_app_type: JupyterServer
      studio_lifecycle_config_content: base64-encoded-content
```
