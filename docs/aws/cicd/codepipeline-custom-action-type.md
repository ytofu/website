# Codepipeline Custom Action Type

Manage Codepipeline Custom Action Type resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codepipeline_custom_action_type:
    example:
      category: Build
      input_artifact_details:
        maximum_count: 1
        minimum_count: 0
      output_artifact_details:
        maximum_count: 1
        minimum_count: 0
      provider_name: example
      version: 1
```
