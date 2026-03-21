# Resource: aws_bedrockagent_agent_knowledge_base_association

ytofu resource for managing an AWS Agents for Amazon Bedrock Agent Knowledge Base Association.

## Basic Example

```yaml
resource:
  aws_bedrockagent_agent_knowledge_base_association:
    example:
      agent_id: GGRRAED6JP
      description: Example Knowledge base
      knowledge_base_id: EMDPPAYPZI
      knowledge_base_state: ENABLED
```

## Argument Reference

The following arguments are required:

* `agent_id` - (Required, Forces new resource) Unique identifier of the agent with which you want to associate the knowledge base.
* `description` - (Required) Description of what the agent should use the knowledge base for.
* `knowledge_base_id` - (Required, Forces new resource) Unique identifier of the knowledge base to associate with the agent.
* `knowledge_base_state` - (Required) Whether to use the knowledge base when sending an [InvokeAgent](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_agent-runtime_InvokeAgent.html) request. Valid values: `ENABLED`, `DISABLED`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `agent_version` - (Optional, Forces new resource) Version of the agent with which you want to associate the knowledge base. Valid values: `DRAFT`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Agent ID, agent version, and knowledge base ID separated by `,`.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_bedrockagent_agent_knowledge_base_association.example GGRRAED6JP,DRAFT,EMDPPAYPZI
```
