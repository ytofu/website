# Resource: aws_connect_lambda_function_association

Provides an Amazon Connect Lambda Function Association. For more information see
[Amazon Connect: Getting Started](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-get-started.html) and [Invoke AWS Lambda functions](https://docs.aws.amazon.com/connect/latest/adminguide/connect-lambda-functions.html).

## Basic Example

```yaml
resource:
  aws_connect_lambda_function_association:
    example:
      function_arn: ${aws_lambda_function.example.arn}
      instance_id: ${aws_connect_instance.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `function_arn` - (Required) Amazon Resource Name (ARN) of the Lambda Function, omitting any version or alias qualifier.
* `instance_id` - (Required) The identifier of the Amazon Connect instance. You can find the instanceId in the ARN of the instance.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Connect instance ID and Lambda Function ARN separated by a comma (`,`).

## Import

```bash
ytofu import aws_connect_lambda_function_association.example aaaaaaaa-bbbb-cccc-dddd-111111111111,arn:aws:lambda:us-west-2:123456789123:function:example
```
