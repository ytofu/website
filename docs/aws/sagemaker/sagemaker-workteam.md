# Sagemaker Workteam

Manage Sagemaker Workteam resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_workteam:
    example:
      workteam_name: example
      workforce_name: ${aws_sagemaker_workforce.example.id}
      description: example
      member_definition:
        cognito_member_definition:
          client_id: ${aws_cognito_user_pool_client.example.id}
          user_pool: ${aws_cognito_user_pool_domain.example.user_pool_id}
          user_group: ${aws_cognito_user_group.example.name}
```

## Oidc Usage

```yaml
resource:
  aws_sagemaker_workteam:
    example:
      workteam_name: example
      workforce_name: ${aws_sagemaker_workforce.example.id}
      description: example
      member_definition:
        oidc_member_definition:
          groups: 
            - example
```
