# Bedrockagentcore Gateway Target

Manage Bedrockagentcore Gateway Target resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    gateway_assume:
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
    gateway_role:
      name: bedrock-gateway-role
      assume_role_policy: ${data.aws_iam_policy_document.gateway_assume.json}

data:
  aws_iam_policy_document:
    lambda_assume:
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
    lambda_role:
      name: example-lambda-role
      assume_role_policy: ${data.aws_iam_policy_document.lambda_assume.json}

resource:
  aws_lambda_function:
    example:
      filename: example.zip
      function_name: example-function
      role: ${aws_iam_role.lambda_role.arn}
      handler: index.handler
      runtime: nodejs20.x

resource:
  aws_bedrockagentcore_gateway:
    example:
      name: example-gateway
      role_arn: ${aws_iam_role.gateway_role.arn}
      authorizer_configuration:
        custom_jwt_authorizer:
          discovery_url: "https://accounts.google.com/.well-known/openid-configuration"

resource:
  aws_bedrockagentcore_gateway_target:
    example:
      name: example-target
      gateway_identifier: ${aws_bedrockagentcore_gateway.example.gateway_id}
      description: Lambda function target for processing requests
      credential_provider_configuration:
        gateway_iam_role:
        target_configuration:
          mcp:
            lambda:
              lambda_arn: ${aws_lambda_function.example.arn}
              tool_schema:
                inline_payload:
                  name: process_request
                  description: Process incoming requests
                  input_schema:
                    type: object
                    description: Request processing schema
                    property:
                      name: message
                      type: string
                      description: Message to process
                      required: true
                    property:
                      name: options
                      type: object
                      property:
                        name: priority
                        type: string
                      property:
                        name: tags
                        type: array
                        items:
                          type: string
                  output_schema:
                    type: object
                    property:
                      name: status
                      type: string
                      required: true
                    property:
                      name: result
                      type: string
```

## Target with API Key Authentication

```yaml
resource:
  aws_bedrockagentcore_gateway_target:
    api_key_example:
      name: api-target
      gateway_identifier: ${aws_bedrockagentcore_gateway.example.gateway_id}
      description: External API target with API key authentication
      credential_provider_configuration:
        api_key:
          provider_arn: "arn:aws:iam::123456789012:oidc-provider/example.com"
          credential_location: HEADER
          credential_parameter_name: X-API-Key
          credential_prefix: Bearer
      target_configuration:
        mcp:
          lambda:
            lambda_arn: ${aws_lambda_function.example.arn}
            tool_schema:
              inline_payload:
                name: api_tool
                description: External API integration tool
                input_schema:
                  type: string
                  description: Simple string input for API calls
```

## Target with OAuth Authentication

```yaml
resource:
  aws_bedrockagentcore_gateway_target:
    oauth_example:
      name: oauth-target
      gateway_identifier: ${aws_bedrockagentcore_gateway.example.gateway_id}
      credential_provider_configuration:
        oauth:
          provider_arn: "arn:aws:iam::123456789012:oidc-provider/oauth.example.com"
          scopes: 
            - read
            - write
          grant_type: authorization_code
          default_return_url: "https://myapp.example.com/callback"
          custom_parameters: 
      target_configuration:
        mcp:
          lambda:
            lambda_arn: ${aws_lambda_function.example.arn}
            tool_schema:
              inline_payload:
                name: oauth_tool
                description: OAuth-authenticated service
                input_schema:
                  type: array
                  items:
                    type: object
                    property:
                      name: id
                      type: string
                      required: true
                    property:
                      name: value
                      type: number
```

## Complex Schema with JSON Serialization

```yaml
resource:
  aws_bedrockagentcore_gateway_target:
    complex_schema:
      name: complex-target
      gateway_identifier: ${aws_bedrockagentcore_gateway.example.gateway_id}
      credential_provider_configuration:
        gateway_iam_role:
        target_configuration:
          mcp:
            lambda:
              lambda_arn: ${aws_lambda_function.example.arn}
              tool_schema:
                inline_payload:
                  name: complex_tool
                  description: Tool with complex nested schema
                  input_schema:
                    type: object
                    property:
                      name: profile
                      type: object
                      property:
                        name: nested_tags
                        type: array
                        items_json: '{ "type": "string" }'
                      property:
                        name: metadata
                        type: object
                        properties_json: '{ "properties": { "created_at" = { "type": "string" } "version" = { "type": "number" } } "required": ["created_at"] }'
```

## MCP Server Target with Header Propagation

```yaml
resource:
  aws_bedrockagentcore_gateway_target:
    mcp_with_headers:
      name: mcp-target-with-headers
      gateway_identifier: ${aws_bedrockagentcore_gateway.example.gateway_id}
      description: MCP server target with header propagation
      target_configuration:
        mcp:
          mcp_server:
            endpoint: "https://example.com/mcp"
      metadata_configuration:
        allowed_request_headers: 
          - x-correlation-id
          - x-tenant-id
        allowed_response_headers: 
          - x-rate-limit-remaining
        allowed_query_parameters: 
          - version
```
