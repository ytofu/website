# Auditmanager Assessment Delegation

Manage Auditmanager Assessment Delegation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_auditmanager_assessment_delegation:
    example:
      assessment_id: ${aws_auditmanager_assessment.example.id}
      role_arn: ${aws_iam_role.example.arn}
      role_type: RESOURCE_OWNER
      control_set_id: example
```
