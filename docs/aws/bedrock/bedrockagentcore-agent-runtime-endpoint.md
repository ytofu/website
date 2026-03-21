# Bedrockagentcore Agent Runtime Endpoint

Manage Bedrockagentcore Agent Runtime Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_agent_runtime_endpoint:
    example:
      name: example-endpoint
      agent_runtime_id: ${aws_bedrockagentcore_agent_runtime.example.agent_runtime_id}
      description: Endpoint for agent runtime communication
```
