# Auditmanager Framework

Manage Auditmanager Framework resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_auditmanager_framework:
    test:
      name: example
      control_sets:
        name: example
        controls:
          id: ${aws_auditmanager_control.test_1.id}
        controls:
          id: ${aws_auditmanager_control.test_2.id}
```
