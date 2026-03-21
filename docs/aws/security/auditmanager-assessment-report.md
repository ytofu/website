# Auditmanager Assessment Report

Manage Auditmanager Assessment Report resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_auditmanager_assessment_report:
    test:
      name: example
      assessment_id: ${aws_auditmanager_assessment.test.id}
```
