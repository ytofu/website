# Swf Domain

Manage Swf Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_swf_domain:
    foo:
      name: foo
      description: Terraform SWF Domain
      workflow_execution_retention_period_in_days: 30
```
