# Resource: aws_codeguruprofiler_profiling_group

ytofu resource for managing an AWS CodeGuru Profiler Profiling Group.

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

## Argument Reference

The following arguments are required:

* `agent_orchestration_config` - (Required) Specifies whether profiling is enabled or disabled for the created profiling. See [Agent Orchestration Config](#agent-orchestration-config) for more details.
* `name` - (Required) Name of the profiling group.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `compute_platform` - (Optional) Compute platform of the profiling group.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the profiling group.
* `id` - Name of the profiling group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

### Agent Orchestration Config

* `profiling_enabled` - (Required) Boolean that specifies whether the profiling agent collects profiling data or

## Import

```bash
ytofu import aws_codeguruprofiler_profiling_group.example profiling_group-name-12345678
```
