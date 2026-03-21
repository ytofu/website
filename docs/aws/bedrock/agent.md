# Bedrock Agent

Create Bedrock agents using ytofu YAML.

## Basic Agent

```yaml
resource:
  aws_bedrockagent_agent:
    example:
      agent_name: example
      agent_resource_role_arn: ${aws_iam_role.bedrock_agent.arn}
      foundation_model: anthropic.claude-3-sonnet-20240229-v1:0
      instruction: You are a helpful assistant.
```
