# Bedrockagentcore Agent Runtime

Manage Bedrockagentcore Agent Runtime resources using ytofu YAML.

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

data:
  aws_iam_policy_document:
    ecr_permissions:
      statement:
        actions: 
          - "ecr:GetAuthorizationToken"
        effect: Allow
        resources: 
          - "*"
      statement:
        actions:
          - "ecr:BatchGetImage"
          - "ecr:GetDownloadUrlForLayer"
        effect: Allow
        resources: 
          - ${aws_ecr_repository.example.arn}

resource:
  aws_iam_role:
    example:
      name: bedrock-agentcore-runtime-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy:
    example:
      role: ${aws_iam_role.example.id}
      policy: ${data.aws_iam_policy_document.ecr_permissions.json}

resource:
  aws_bedrockagentcore_agent_runtime:
    example:
      agent_runtime_name: example_agent_runtime
      role_arn: ${aws_iam_role.example.arn}
      agent_runtime_artifact:
        container_configuration:
          container_uri: "${aws_ecr_repository.example.repository_url}:latest"
      network_configuration:
        network_mode: PUBLIC
```

## MCP Server With Custom JWT Authorizer

```yaml
resource:
  aws_bedrockagentcore_agent_runtime:
    example:
      agent_runtime_name: example_agent_runtime
      description: Agent runtime with JWT authorization
      role_arn: ${aws_iam_role.example.arn}
      agent_runtime_artifact:
        container_configuration:
          container_uri: "${aws_ecr_repository.example.repository_url}:v1.0"
      environment_variables:
        LOG_LEVEL: INFO
        ENV: production
      authorizer_configuration:
        custom_jwt_authorizer:
          discovery_url: "https://accounts.google.com/.well-known/openid-configuration"
          allowed_audience: 
            - my-app
            - mobile-app
          allowed_clients: 
            - client-123
            - client-456
          allowed_scopes: 
            - openid
            - email
      network_configuration:
        network_mode: PUBLIC
      protocol_configuration:
        server_protocol: MCP
```

## Agent runtime artifact from S3 with Code Configuration

```yaml
resource:
  aws_bedrockagentcore_agent_runtime:
    example:
      agent_runtime_name: example_agent_runtime
      role_arn: ${aws_iam_role.example.arn}
      agent_runtime_artifact:
        code_configuration:
          entry_point: 
            - main.py
          runtime: PYTHON_3_13
          code:
            s3:
              bucket: example-bucket
              prefix: example-agent-runtime-code.zip
      network_configuration:
        network_mode: PUBLIC
```
