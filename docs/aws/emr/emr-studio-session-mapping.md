# EMR Studio Session Mapping

Manage EMR Studio Session Mapping resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emr_studio_session_mapping:
    example:
      studio_id: ${aws_emr_studio.example.id}
      identity_type: USER
      identity_id: example
      session_policy_arn: ${aws_iam_policy.example.arn}
```
