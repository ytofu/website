# Resource: aws_lambda_permission

Manages an AWS Lambda permission. Use this resource to grant external sources (e.g., EventBridge Rules, SNS, or S3) permission to invoke Lambda functions.

## Basic Example

```yaml
resource:
  aws_lambda_permission:
    allow_cloudwatch:
      statement_id: AllowExecutionFromCloudWatch
      action: "lambda:InvokeFunction"
      function_name: ${aws_lambda_function.test_lambda.function_name}
      principal: events.amazonaws.com
      source_arn: "arn:aws:events:eu-west-1:111122223333:rule/RunDaily"
      qualifier: ${aws_lambda_alias.test_alias.name}

  aws_lambda_alias:
    test_alias:
      name: testalias
      description: a sample description
      function_name: ${aws_lambda_function.test_lambda.function_name}
      function_version: $LATEST

  aws_lambda_function:
    test_lambda:
      filename: lambdatest.zip
      function_name: lambda_function_name
      role: ${aws_iam_role.iam_for_lambda.arn}
      handler: exports.handler
      runtime: nodejs20.x

  aws_iam_role:
    iam_for_lambda:
      name: iam_for_lambda
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "lambda.amazonaws.com" } } ] }'```

## SNS Integration

```yaml
resource:
  aws_lambda_permission:
    with_sns:
      statement_id: AllowExecutionFromSNS
      action: "lambda:InvokeFunction"
      function_name: ${aws_lambda_function.func.function_name}
      principal: sns.amazonaws.com
      source_arn: ${aws_sns_topic.default.arn}

  aws_sns_topic:
    default:
      name: call-lambda-maybe

  aws_sns_topic_subscription:
    lambda:
      topic_arn: ${aws_sns_topic.default.arn}
      protocol: lambda
      endpoint: ${aws_lambda_function.func.arn}

  aws_lambda_function:
    func:
      filename: lambdatest.zip
      function_name: lambda_called_from_sns
      role: ${aws_iam_role.default.arn}
      handler: exports.handler
      runtime: python3.12

  aws_iam_role:
    default:
      name: iam_for_lambda_with_sns
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "lambda.amazonaws.com" } } ] }'```

## API Gateway REST API Integration

```yaml
resource:
  aws_api_gateway_rest_api:
    MyDemoAPI:
      name: MyDemoAPI
      description: This is my API for demonstration purposes

  aws_lambda_permission:
    lambda_permission:
      statement_id: AllowMyDemoAPIInvoke
      action: "lambda:InvokeFunction"
      function_name: MyDemoFunction
      principal: apigateway.amazonaws.com
      source_arn: "${aws_api_gateway_rest_api.MyDemoAPI.execution_arn}/*"```

## CloudWatch Log Group Integration

```yaml
resource:
  aws_lambda_permission:
    logging:
      action: "lambda:InvokeFunction"
      function_name: ${aws_lambda_function.logging.function_name}
      principal: logs.eu-west-1.amazonaws.com
      source_arn: "${aws_cloudwatch_log_group.default.arn}:*"

  aws_cloudwatch_log_group:
    default:
      name: /default

  aws_cloudwatch_log_subscription_filter:
    logging:
      depends_on: 
        - ${aws_lambda_permission.logging}
      destination_arn: ${aws_lambda_function.logging.arn}
      filter_pattern: 
      log_group_name: ${aws_cloudwatch_log_group.default.name}
      name: logging_default

  aws_lambda_function:
    logging:
      filename: lamba_logging.zip
      function_name: lambda_called_from_cloudwatch_logs
      handler: exports.handler
      role: ${aws_iam_role.default.arn}
      runtime: python3.12

  aws_iam_role:
    default:
      name: iam_for_lambda_called_from_cloudwatch_logs
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - lambda.amazonaws.com
        actions: 
          - "sts:AssumeRole"```

## Cross-Account Function URL Access

```yaml
resource:
  aws_lambda_function_url:
    url:
      function_name: ${aws_lambda_function.example.function_name}
      authorization_type: AWS_IAM

  aws_lambda_permission:
    url:
      action: "lambda:InvokeFunctionUrl"
      function_name: ${aws_lambda_function.example.function_name}
      principal: "arn:aws:iam::444455556666:role/example"
      source_account: 444455556666
      function_url_auth_type: AWS_IAM```

## Automatic Permission Updates with Function Changes

```yaml
resource:
  aws_lambda_permission:
    logging:
      action: "lambda:InvokeFunction"
      function_name: ${aws_lambda_function.example.function_name}
      principal: events.amazonaws.com
      source_arn: "arn:aws:events:eu-west-1:111122223333:rule/RunDaily"
      lifecycle:
        replace_triggered_by:
          - ${aws_lambda_function.example}
```

## Argument Reference

The following arguments are required:

* `action` - (Required) Lambda action to allow in this statement (e.g., `lambda:InvokeFunction`)
* `function_name` - (Required) Name or ARN of the Lambda function
* `principal` - (Required) AWS service or account that invokes the function (e.g., `s3.amazonaws.com`, `sns.amazonaws.com`, AWS account ID, or AWS IAM principal)

The following arguments are optional:

* `event_source_token` - (Optional) Event Source Token for Alexa Skills
* `function_url_auth_type` - (Optional) Lambda Function URL authentication type. Valid values: `AWS_IAM` or `NONE`. Only valid with `lambda:InvokeFunctionUrl` action
* `invoked_via_function_url` (Optional) Lambda Function URL invoke permission. Only valid with `lambda:InvokeFunction` action
* `principal_org_id` - (Optional) AWS Organizations ID to grant permission to all accounts under this organization
* `qualifier` - (Optional) Lambda function version or alias name
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration
* `source_account` - (Optional) AWS account ID of the source owner for cross-account access, S3, or SES
* `source_arn` - (Optional) ARN of the source resource granting permission to invoke the Lambda function
* `statement_id` - (Optional) Statement identifier. Generated by ytofu if not provided
* `statement_id_prefix` - (Optional) Statement identifier prefix. Conflicts with `statement_id`

## Attribute Reference

This resource exports no additional attributes.
