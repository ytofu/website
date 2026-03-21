# Sagemaker Endpoint

Manage Sagemaker Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_endpoint:
    e:
      name: my-endpoint
      endpoint_config_name: ${aws_sagemaker_endpoint_configuration.ec.name}
      tags:
        Name: foo
```
