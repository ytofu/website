# Lambda Capacity Provider

Manage Lambda Capacity Provider resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_capacity_provider:
    example:
      name: example
      vpc_config:
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: 
          - ${aws_security_group.example.id}
      permissions_config:
        capacity_provider_operator_role_arn: ${aws_iam_role.example.arn}
```

## Manual Scaling with Specific Instance Types

```yaml
resource:
  aws_lambda_capacity_provider:
    example:
      name: example
      vpc_config:
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: 
          - ${aws_security_group.example.id}
      permissions_config:
        capacity_provider_operator_role_arn: ${aws_iam_role.example.arn}
      instance_requirements:
        architectures: 
          - x86_64
        allowed_instance_types: 
          - c6i.2xlarge
          - c7i.2xlarge
      capacity_provider_scaling_config:
        scaling_mode: Manual
        scaling_policies:
          - predefined_metric_type: LambdaCapacityProviderAverageCPUUtilization
```
