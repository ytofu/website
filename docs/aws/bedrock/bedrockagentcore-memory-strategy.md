# Bedrockagentcore Memory Strategy

Manage Bedrockagentcore Memory Strategy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_memory_strategy:
    semantic:
      name: semantic-strategy
      memory_id: ${aws_bedrockagentcore_memory.example.id}
      type: SEMANTIC
      description: Semantic understanding strategy
      namespaces: 
        - default
```

## Summarization Strategy

```yaml
resource:
  aws_bedrockagentcore_memory_strategy:
    summary:
      name: summary-strategy
      memory_id: ${aws_bedrockagentcore_memory.example.id}
      type: SUMMARIZATION
      description: Text summarization strategy
      namespaces: 
        - "{sessionId}"
```

## User Preference Strategy

```yaml
resource:
  aws_bedrockagentcore_memory_strategy:
    user_pref:
      name: user-preference-strategy
      memory_id: ${aws_bedrockagentcore_memory.example.id}
      type: USER_PREFERENCE
      description: User preference tracking strategy
      namespaces: 
        - preferences
```

## Custom Strategy with Semantic Override

```yaml
resource:
  aws_bedrockagentcore_memory_strategy:
    custom_semantic:
      name: custom-semantic-strategy
      memory_id: ${aws_bedrockagentcore_memory.example.id}
      memory_execution_role_arn: ${aws_bedrockagentcore_memory.example.memory_execution_role_arn}
      type: CUSTOM
      description: Custom semantic processing strategy
      namespaces: 
        - "{sessionId}"
      configuration:
        type: SEMANTIC_OVERRIDE
        consolidation:
          append_to_prompt: Focus on extracting key semantic relationships and concepts
          model_id: "anthropic.claude-3-sonnet-20240229-v1:0"
        extraction:
          append_to_prompt: Extract and categorize semantic information
          model_id: "anthropic.claude-3-haiku-20240307-v1:0"
```

## Custom Strategy with Summary Override

```yaml
resource:
  aws_bedrockagentcore_memory_strategy:
    custom_summary:
      name: custom-summary-strategy
      memory_id: ${aws_bedrockagentcore_memory.example.id}
      type: CUSTOM
      description: Custom summarization strategy
      namespaces: 
        - summaries
      configuration:
        type: SUMMARY_OVERRIDE
        consolidation:
          append_to_prompt: Create concise summaries while preserving key details
          model_id: "anthropic.claude-3-sonnet-20240229-v1:0"
```

## Custom Strategy with User Preference Override

```yaml
resource:
  aws_bedrockagentcore_memory_strategy:
    custom_user_pref:
      name: custom-user-preference-strategy
      memory_id: ${aws_bedrockagentcore_memory.example.id}
      type: CUSTOM
      description: Custom user preference tracking strategy
      namespaces: 
        - user_prefs
      configuration:
        type: USER_PREFERENCE_OVERRIDE
        consolidation:
          append_to_prompt: Consolidate user preferences and behavioral patterns
          model_id: "anthropic.claude-3-sonnet-20240229-v1:0"
        extraction:
          append_to_prompt: Extract user preferences and interaction patterns
          model_id: "anthropic.claude-3-haiku-20240307-v1:0"
```
