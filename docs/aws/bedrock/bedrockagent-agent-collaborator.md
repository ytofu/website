# Bedrockagent Agent Collaborator

Manage Bedrockagent Agent Collaborator resources using ytofu YAML.

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
          - "arn:${data.aws_partition.current.partition}:bedrock:${data.aws_region.current.region}::foundation-model/anthropic.claude-3-5-sonnet-20241022-v2:0"
      statement:
        actions: 
          - "bedrock:GetAgentAlias"
          - "bedrock:InvokeAgent"
        resources:
          - "arn:${data.aws_partition.current_agent.partition}:bedrock:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:agent/*"
          - "arn:${data.aws_partition.current_agent.partition}:bedrock:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:agent-alias/*"

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
    example_collaborator:
      agent_name: my-agent-collaborator
      agent_resource_role_arn: ${aws_iam_role.example.arn}
      idle_session_ttl_in_seconds: 500
      foundation_model: "anthropic.claude-3-5-sonnet-20241022-v2:0"
      instruction: do what the supervisor tells you to do

resource:
  aws_bedrockagent_agent:
    example_supervisor:
      agent_name: my-agent-supervisor
      agent_resource_role_arn: ${aws_iam_role.example.arn}
      agent_collaboration: SUPERVISOR
      idle_session_ttl_in_seconds: 500
      foundation_model: "anthropic.claude-3-5-sonnet-20241022-v2:0"
      instruction: tell the sub agent what to do
      prepare_agent: false

resource:
  aws_bedrockagent_agent_alias:
    example:
      agent_alias_name: my-agent-alias
      agent_id: ${aws_bedrockagent_agent.example_collaborator.agent_id}
      description: Test Alias

resource:
  aws_bedrockagent_agent_collaborator:
    example:
      agent_id: ${aws_bedrockagent_agent.example_supervisor.agent_id}
      collaboration_instruction: tell the other agent what to do
      collaborator_name: my-collab-example
      relay_conversation_history: TO_COLLABORATOR
      agent_descriptor:
        alias_arn: ${aws_bedrockagent_agent_alias.example.agent_alias_arn}
```
