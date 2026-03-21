# API Gateway Authorizer

Manage API Gateway Authorizer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_authorizer:
    demo:
      name: demo
      rest_api_id: ${aws_api_gateway_rest_api.demo.id}
      authorizer_uri: ${aws_lambda_function.authorizer.invoke_arn}
      authorizer_credentials: ${aws_iam_role.invocation_role.arn}

resource:
  aws_api_gateway_rest_api:
    demo:
      name: auth-demo

data:
  aws_iam_policy_document:
    invocation_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - apigateway.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    invocation_role:
      name: api_gateway_auth_invocation
      path: /
      assume_role_policy: ${data.aws_iam_policy_document.invocation_assume_role.json}

data:
  aws_iam_policy_document:
    invocation_policy:
      statement:
        effect: Allow
        actions: 
          - "lambda:InvokeFunction"
        resources: 
          - ${aws_lambda_function.authorizer.arn}

resource:
  aws_iam_role_policy:
    invocation_policy:
      name: default
      role: ${aws_iam_role.invocation_role.id}
      policy: ${data.aws_iam_policy_document.invocation_policy.json}

data:
  aws_iam_policy_document:
    lambda_assume_role:
      statement:
        effect: Allow
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - lambda.amazonaws.com

resource:
  aws_iam_role:
    lambda:
      name: demo-lambda
      assume_role_policy: ${data.aws_iam_policy_document.lambda_assume_role.json}

resource:
  aws_lambda_function:
    authorizer:
      filename: lambda-function.zip
      function_name: api_gateway_authorizer
      role: ${aws_iam_role.lambda.arn}
      handler: exports.example
      source_code_hash: ${filebase64sha256("lambda-function.zip")}
```
