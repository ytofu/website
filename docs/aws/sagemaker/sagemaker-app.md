# Sagemaker App

Manage Sagemaker App resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_app:
    example:
      domain_id: ${aws_sagemaker_domain.example.id}
      user_profile_name: ${aws_sagemaker_user_profile.example.user_profile_name}
      app_name: example
      app_type: JupyterServer
```
