# Resource: aws_lambda_layer_version_permission

Manages an AWS Lambda Layer Version Permission. Use this resource to share Lambda Layers with other AWS accounts, organizations, or make them publicly accessible.

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

## Argument Reference

The following arguments are required:

* `action` - (Required) Action that will be allowed. `lambda:GetLayerVersion` is the standard value for layer access.
* `layer_name` - (Required) Name or ARN of the Lambda Layer.
* `principal` - (Required) AWS account ID that should be able to use your Lambda Layer. Use `*` to share with all AWS accounts.
* `statement_id` - (Required) Unique identifier for the permission statement.
* `version_number` - (Required) Version of Lambda Layer to grant access to. Note: permissions only apply to a single version of a layer.

The following arguments are optional:

* `organization_id` - (Optional) AWS Organization ID that should be able to use your Lambda Layer. `principal` should be set to `*` when `organization_id` is provided.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `skip_destroy` - (Optional) Whether to retain the permission when the resource is destroyed. Default is `false`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Layer name and version number, separated by a comma (`,`).
* `policy` - Full Lambda Layer Permission policy.
* `revision_id` - Unique identifier for the current revision of the policy.
