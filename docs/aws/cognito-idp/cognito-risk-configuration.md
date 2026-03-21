# Cognito Risk Configuration

Manage Cognito Risk Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_risk_configuration:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      risk_exception_configuration:
        blocked_ip_range_list: 
          - 10.10.10.10/32
```
