# Auditmanager Control

Manage Auditmanager Control resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_auditmanager_control:
    example:
      name: example
      control_mapping_sources:
        source_name: example
        source_set_up_option: Procedural_Controls_Mapping
        source_type: MANUAL
```
