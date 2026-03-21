# Sagemaker App Image Config

Manage Sagemaker App Image Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_app_image_config:
    test:
      app_image_config_name: example
      kernel_gateway_image_config:
        kernel_spec:
          name: example
```

## Using Code Editor with empty configuration

```yaml
resource:
  aws_sagemaker_app_image_config:
    test:
      app_image_config_name: example
      code_editor_app_image_config:
```

## Default File System Config

```yaml
resource:
  aws_sagemaker_app_image_config:
    test:
      app_image_config_name: example
      kernel_gateway_image_config:
        kernel_spec:
          name: example
        file_system_config:
```
