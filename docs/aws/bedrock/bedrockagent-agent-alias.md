# Bedrockagent Agent Alias

Manage Bedrockagent Agent Alias resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

data:
  aws_region:
    current:

data:
  aws_iam_policy_document:
    example_agent_trust:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          identifiers: 
            - bedrock.amazonaws.com
          type: Service
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}
        condition:
          test: ArnLike
          values: 
            - "arn:${data.aws_partition.current.partition}:bedrock:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:agent/*"

data:
  aws_iam_policy_document:
    example_agent_permissions:
      statement:
        actions: 
          - "bedrock:InvokeModel"
        resources:
          - "arn:${data.aws_partition.current.partition}:bedrock:${data.aws_region.current.region}::foundation-model/anthropic.claude-v2"

resource:
  aws_iam_role:
    example:
      assume_role_policy: ${data.aws_iam_policy_document.example_agent_trust.json}
      name_prefix: AmazonBedrockExecutionRoleForAgents_

resource:
  aws_iam_role_policy:
    example:
      policy: ${data.aws_iam_policy_document.example_agent_permissions.json}
      role: ${aws_iam_role.example.id}

resource:
  aws_bedrockagent_agent:
    example:
      agent_name: my-agent-name
      agent_resource_role_arn: ${aws_iam_role.example.arn}
      idle_ttl: 500
      foundation_model: anthropic.claude-v2

resource:
  aws_bedrockagent_agent_alias:
    example:
      agent_alias_name: my-agent-alias
      agent_id: ${aws_bedrockagent_agent.example.agent_id}
      description: Test Alias
```
