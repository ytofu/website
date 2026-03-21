# Ssoadmin Application Assignment Configuration

Manage Ssoadmin Application Assignment Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssoadmin_application_assignment_configuration:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      assignment_required: true
```
