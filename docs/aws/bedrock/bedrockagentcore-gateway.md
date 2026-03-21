# Bedrockagentcore Gateway

Manage Bedrockagentcore Gateway resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - bedrock-agentcore.amazonaws.com

resource:
  aws_iam_role:
    example:
      name: bedrock-agentcore-gateway-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_bedrockagentcore_gateway:
    example:
      name: example-gateway
      role_arn: ${aws_iam_role.example.arn}
      authorizer_type: CUSTOM_JWT
      authorizer_configuration:
        custom_jwt_authorizer:
          discovery_url: "https://accounts.google.com/.well-known/openid-configuration"
          allowed_audience: 
            - test1
            - test2
      protocol_type: MCP
```

## Gateway with advanced JWT Authorization and MCP Configuration

```yaml
resource:
  aws_bedrockagentcore_gateway:
    example:
      name: mcp-gateway
      description: Gateway for MCP communication
      role_arn: ${aws_iam_role.example.arn}
      authorizer_type: CUSTOM_JWT
      authorizer_configuration:
        custom_jwt_authorizer:
          discovery_url: "https://auth.example.com/.well-known/openid-configuration"
          allowed_audience: 
            - app-client
            - web-client
          allowed_clients: 
            - client-123
            - client-456
          allowed_scopes: 
            - openid
            - email
      protocol_type: MCP
      protocol_configuration:
        mcp:
          instructions: Gateway for handling MCP requests
          search_type: HYBRID
          supported_versions: 
            - 2025-03-26
            - 2025-06-18
```

## Gateway with Interceptor Configuration

```yaml
resource:
  aws_lambda_function:
    interceptor:
      filename: interceptor.zip
      function_name: gateway-interceptor
      role: ${aws_iam_role.lambda.arn}
      handler: index.handler
      runtime: python3.12

resource:
  aws_bedrockagentcore_gateway:
    example:
      name: gateway-with-interceptor
      role_arn: ${aws_iam_role.example.arn}
      authorizer_type: AWS_IAM
      protocol_type: MCP
      interceptor_configuration:
        interception_points: 
          - REQUEST
          - RESPONSE
        interceptor:
          lambda:
            arn: ${aws_lambda_function.interceptor.arn}
        input_configuration:
          pass_request_headers: true
```
