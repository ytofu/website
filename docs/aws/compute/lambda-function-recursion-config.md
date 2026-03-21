# Resource: aws_lambda_function_recursion_config

Manages an AWS Lambda Function Recursion Config. Use this resource to control how Lambda handles recursive function invocations to prevent infinite loops.

## Basic Example

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: recursive_processor
      role: ${aws_iam_role.lambda_role.arn}
      handler: index.handler
      runtime: python3.12

resource:
  aws_lambda_function_recursion_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      recursive_loop: Allow
```

## Production Safety Configuration

```yaml
resource:
  aws_lambda_function:
    production_processor:
      filename: processor.zip
      function_name: production-data-processor
      role: ${aws_iam_role.lambda_role.arn}
      handler: app.handler
      runtime: nodejs20.x
      tags:
        Environment: production
        Purpose: data-processing

resource:
  aws_lambda_function_recursion_config:
    example:
      function_name: ${aws_lambda_function.production_processor.function_name}
      recursive_loop: "Terminate" # Safety first in production
```

## Argument Reference

The following arguments are required:

* `function_name` - (Required) Name of the Lambda function.
* `recursive_loop` - (Required) Lambda function recursion configuration. Valid values are `Allow` or `Terminate`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.
