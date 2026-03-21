# Resource: aws_lambda_invocation

Manages an AWS Lambda Function invocation. Use this resource to invoke a Lambda function with the [RequestResponse](https://docs.aws.amazon.com/lambda/latest/dg/API_Invoke.html#API_Invoke_RequestSyntax) invocation type.

## Basic Example

```yaml
resource:
  aws_lambda_function:
    example:
      filename: function.zip
      function_name: data_processor
      role: ${aws_iam_role.lambda_role.arn}
      handler: index.handler
      runtime: python3.12

  aws_lambda_invocation:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      input: '{ "operation": "initialize" "config": { "environment": "production" "debug": false } }'

output:
  initialization_result:
    value: ${jsondecode(aws_lambda_invocation.example.result)["status"]}```

## Dynamic Invocation with Triggers

```yaml
resource:
  aws_lambda_invocation:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      triggers:
        function_version: ${aws_lambda_function.example.version}
        config_hash: example-config-hash
      input: '{ "operation": "process_data" "environment": var.environment "batch_id": random_uuid.batch_id.result }'
```

## CRUD Lifecycle Management

```yaml
resource:
  aws_lambda_invocation:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      input: '{ "resource_name": "database_setup" "database_url": aws_db_instance.example.endpoint "credentials": { "username": var.db_username "password": var.db_password } }'
      lifecycle_scope: CRUD
```

## Argument Reference

The following arguments are required:

* `function_name` - (Required) Name of the Lambda function.
* `input` - (Required) JSON payload to the Lambda function.

The following arguments are optional:

* `lifecycle_scope` - (Optional) Lifecycle scope of the resource to manage. Valid values are `CREATE_ONLY` and `CRUD`. Defaults to `CREATE_ONLY`. `CREATE_ONLY` will invoke the function only on creation or replacement. `CRUD` will invoke the function on each lifecycle event, and augment the input JSON payload with additional lifecycle information.
* `qualifier` - (Optional) Qualifier (i.e., version) of the Lambda function. Defaults to `$LATEST`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tenant_id` - (Optional) Tenant Id to serve invocations from specified tenant.
* `terraform_key` - (Optional) JSON key used to store lifecycle information in the input JSON payload. Defaults to `tf`. This additional key is only included when `lifecycle_scope` is set to `CRUD`.
* `triggers` - (Optional) Map of arbitrary keys and values that, when changed, will trigger a re-invocation. To force a re-invocation without changing these keys/values, use the `ytofu taint` command.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `result` - String result of the Lambda function invocation.

## Import

```bash
ytofu import aws_lambda_invocation.test_lambda my_test_lambda_function,$LATEST,b326b5062b2f0e69046810717534cb09
```
