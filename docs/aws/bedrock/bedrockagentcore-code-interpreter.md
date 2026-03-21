# Bedrockagentcore Code Interpreter

Manage Bedrockagentcore Code Interpreter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_code_interpreter:
    example:
      name: example-code-interpreter
      description: Code interpreter for data analysis
      network_configuration:
        network_mode: PUBLIC
```

## Code Interpreter with Execution Role

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
      name: bedrock-agentcore-code-interpreter-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_bedrockagentcore_code_interpreter:
    example:
      name: example-code-interpreter
      description: Code interpreter with custom execution role
      execution_role_arn: ${aws_iam_role.example.arn}
      network_configuration:
        network_mode: SANDBOX
```
