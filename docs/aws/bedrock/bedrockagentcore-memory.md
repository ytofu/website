# Bedrockagentcore Memory

Manage Bedrockagentcore Memory resources using ytofu YAML.

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
      name: bedrock-agentcore-memory-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.example.name}
      policy_arn: "arn:aws:iam::aws:policy/AmazonBedrockAgentCoreMemoryBedrockModelInferenceExecutionRolePolicy"

resource:
  aws_bedrockagentcore_memory:
    example:
      name: example_memory
      event_expiry_duration: 30
```

## Memory with Custom Encryption and Role

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS key for Bedrock AgentCore Memory

resource:
  aws_bedrockagentcore_memory:
    example:
      name: example_memory
      description: Memory for customer service agent
      event_expiry_duration: 60
      encryption_key_arn: ${aws_kms_key.example.arn}
      memory_execution_role_arn: ${aws_iam_role.example.arn}
      client_token: unique-client-token
```
