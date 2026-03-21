# Codeguruprofiler Profiling Group

Manage Codeguruprofiler Profiling Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codeguruprofiler_profiling_group:
    example:
      name: example
      compute_platform: Default
      agent_orchestration_config:
        profiling_enabled: true
```
