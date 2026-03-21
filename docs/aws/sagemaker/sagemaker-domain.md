# Sagemaker Domain

Manage Sagemaker Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_domain:
    example:
      domain_name: example
      auth_mode: IAM
      vpc_id: ${aws_vpc.example.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
      default_user_settings:
        execution_role: ${aws_iam_role.example.arn}

resource:
  aws_iam_role:
    example:
      name: example
      path: /
      assume_role_policy: ${data.aws_iam_policy_document.example.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - sagemaker.amazonaws.com
```

## Using Custom Images

```yaml
resource:
  aws_sagemaker_image:
    example:
      image_name: example
      role_arn: ${aws_iam_role.example.arn}

resource:
  aws_sagemaker_app_image_config:
    example:
      app_image_config_name: example
      kernel_gateway_image_config:
        kernel_spec:
          name: example

resource:
  aws_sagemaker_image_version:
    example:
      image_name: ${aws_sagemaker_image.example.id}
      base_image: base-image

resource:
  aws_sagemaker_domain:
    example:
      domain_name: example
      auth_mode: IAM
      vpc_id: ${aws_vpc.example.id}
      subnet_ids: 
        - ${aws_subnet.example.id}
      default_user_settings:
        execution_role: ${aws_iam_role.example.arn}
        kernel_gateway_app_settings:
          custom_image:
            app_image_config_name: ${aws_sagemaker_app_image_config.example.app_image_config_name}
            image_name: ${aws_sagemaker_image_version.example.image_name}
```
