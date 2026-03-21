# Resource: aws_lambda_runtime_management_config

Manages an AWS Lambda Runtime Management Config. Use this resource to control how Lambda updates the runtime for your function.

## Basic Example

```yaml
resource:
  aws_lambda_runtime_management_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      update_runtime_on: FunctionUpdate
```

## Manual Update

```yaml
resource:
  aws_lambda_runtime_management_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      update_runtime_on: Manual
      runtime_version_arn: "arn:aws:lambda:us-east-1::runtime:abcd1234"
```

## Argument Reference

The following arguments are required:

* `function_name` - (Required) Name or ARN of the Lambda function.

The following arguments are optional:

* `qualifier` - (Optional) Version of the function. This can be `$LATEST` or a published version number. If omitted, this resource will manage the runtime configuration for `$LATEST`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `runtime_version_arn` - (Optional) ARN of the runtime version. Only required when `update_runtime_on` is `Manual`.
* `update_runtime_on` - (Optional) Runtime update mode. Valid values are `Auto`, `FunctionUpdate`, and `Manual`. When a function is created, the default mode is `Auto`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `function_arn` - ARN of the function.

## Import

```bash
ytofu import aws_lambda_runtime_management_config.example example,$LATEST
```
