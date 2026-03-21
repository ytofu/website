# SFN State Machine

Manage SFN State Machine resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sfn_state_machine:
    sfn_state_machine:
      name: my-state-machine
      role_arn: ${aws_iam_role.iam_for_sfn.arn}
      definition: |
        {
        "Comment": "A Hello World example of the Amazon States Language using an AWS Lambda Function",
        "StartAt": "HelloWorld",
        "States": {
        "HelloWorld": {
        "Type": "Task",
        "Resource": "${aws_lambda_function.lambda.arn}",
        "End": true
        }
        }
        }
```

## Basic (Express Workflow)

```yaml
resource:
  aws_sfn_state_machine:
    sfn_state_machine:
      name: my-state-machine
      role_arn: ${aws_iam_role.iam_for_sfn.arn}
      type: EXPRESS
      definition: |
        {
        "Comment": "A Hello World example of the Amazon States Language using an AWS Lambda Function",
        "StartAt": "HelloWorld",
        "States": {
        "HelloWorld": {
        "Type": "Task",
        "Resource": "${aws_lambda_function.lambda.arn}",
        "End": true
        }
        }
        }
```

## Publish (Publish SFN version)

```yaml
resource:
  aws_sfn_state_machine:
    sfn_state_machine:
      name: my-state-machine
      role_arn: ${aws_iam_role.iam_for_sfn.arn}
      publish: true
      type: EXPRESS
      definition: |
        {
        "Comment": "A Hello World example of the Amazon States Language using an AWS Lambda Function",
        "StartAt": "HelloWorld",
        "States": {
        "HelloWorld": {
        "Type": "Task",
        "Resource": "${aws_lambda_function.lambda.arn}",
        "End": true
        }
        }
        }
```

## Logging

```yaml
resource:
  aws_sfn_state_machine:
    sfn_state_machine:
      name: my-state-machine
      role_arn: ${aws_iam_role.iam_for_sfn.arn}
      definition: |
        {
        "Comment": "A Hello World example of the Amazon States Language using an AWS Lambda Function",
        "StartAt": "HelloWorld",
        "States": {
        "HelloWorld": {
        "Type": "Task",
        "Resource": "${aws_lambda_function.lambda.arn}",
        "End": true
        }
        }
        }
      logging_configuration:
        log_destination: "${aws_cloudwatch_log_group.log_group_for_sfn.arn}:*"
        include_execution_data: true
        level: ERROR
```

## Encryption

```yaml
resource:
  aws_sfn_state_machine:
    sfn_state_machine:
      name: my-state-machine
      role_arn: ${aws_iam_role.iam_for_sfn.arn}
      definition: |
        {
        "Comment": "A Hello World example of the Amazon States Language using an AWS Lambda Function",
        "StartAt": "HelloWorld",
        "States": {
        "HelloWorld": {
        "Type": "Task",
        "Resource": "${aws_lambda_function.lambda.arn}",
        "End": true
        }
        }
        }
      encryption_configuration:
        kms_key_id: ${aws_kms_key.kms_key_for_sfn.arn}
        type: CUSTOMER_MANAGED_KMS_KEY
        kms_data_key_reuse_period_seconds: 900
```
