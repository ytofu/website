# Resource: aws_lambda_provisioned_concurrency_config

Manages an AWS Lambda Provisioned Concurrency Configuration. Use this resource to configure provisioned concurrency for Lambda functions.

## Basic Example

```yaml
resource:
  aws_lambda_provisioned_concurrency_config:
    example:
      function_name: ${aws_lambda_alias.example.function_name}
      provisioned_concurrent_executions: 1
      qualifier: ${aws_lambda_alias.example.name}
```

## Function Version

```yaml
resource:
  aws_lambda_provisioned_concurrency_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      provisioned_concurrent_executions: 1
      qualifier: ${aws_lambda_function.example.version}
```

## Argument Reference

The following arguments are required:

* `function_name` - (Required) Name or Amazon Resource Name (ARN) of the Lambda Function.
* `provisioned_concurrent_executions` - (Required) Amount of capacity to allocate. Must be greater than or equal to 1.
* `qualifier` - (Required) Lambda Function version or Lambda Alias name.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `skip_destroy` - (Optional) Whether to retain the provisioned concurrency configuration upon destruction. Defaults to `false`. If set to `true`, the resource is simply removed from state instead.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Lambda Function name and qualifier separated by a comma (`,`).

## Timeouts

Configuration options:

* `create` - (Default `15m`)
* `update` - (Default `15m`)

## Import

```bash
ytofu import aws_lambda_provisioned_concurrency_config.example example,production
```
