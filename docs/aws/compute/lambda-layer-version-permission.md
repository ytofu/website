# Lambda Layer Version Permission

Manage Lambda Layer Version Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_layer_version:
    example:
      filename: layer.zip
      layer_name: shared_utilities
      description: Common utilities for Lambda functions
      compatible_runtimes: 
        - nodejs20.x
        - python3.12

resource:
  aws_lambda_layer_version_permission:
    example:
      layer_name: ${aws_lambda_layer_version.example.layer_name}
      version_number: ${aws_lambda_layer_version.example.version}
      principal: "123456789012" # Target AWS account ID
      action: "lambda:GetLayerVersion"
      statement_id: dev-account-access
```

## Share Layer with Organization

```yaml
resource:
  aws_lambda_layer_version_permission:
    example:
      layer_name: ${aws_lambda_layer_version.example.layer_name}
      version_number: ${aws_lambda_layer_version.example.version}
      principal: "*"
      organization_id: "o-1234567890" # AWS Organization ID
      action: "lambda:GetLayerVersion"
      statement_id: org-wide-access
```

## Share Layer Publicly

```yaml
resource:
  aws_lambda_layer_version_permission:
    example:
      layer_name: ${aws_lambda_layer_version.example.layer_name}
      version_number: ${aws_lambda_layer_version.example.version}
      principal: "*" # All AWS accounts
      action: "lambda:GetLayerVersion"
      statement_id: public-access
```

## Multiple Account Access

```yaml
resource:
  aws_lambda_layer_version_permission:
    dev_account:
      layer_name: ${aws_lambda_layer_version.example.layer_name}
      version_number: ${aws_lambda_layer_version.example.version}
      principal: 111111111111
      action: "lambda:GetLayerVersion"
      statement_id: dev-account

resource:
  aws_lambda_layer_version_permission:
    staging_account:
      layer_name: ${aws_lambda_layer_version.example.layer_name}
      version_number: ${aws_lambda_layer_version.example.version}
      principal: 222222222222
      action: "lambda:GetLayerVersion"
      statement_id: staging-account

resource:
  aws_lambda_layer_version_permission:
    prod_account:
      layer_name: ${aws_lambda_layer_version.example.layer_name}
      version_number: ${aws_lambda_layer_version.example.version}
      principal: 333333333333
      action: "lambda:GetLayerVersion"
      statement_id: prod-account
```
