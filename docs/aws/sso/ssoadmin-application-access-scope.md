# Ssoadmin Application Access Scope

Manage Ssoadmin Application Access Scope resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_ssoadmin_application:
    example:
      name: example
      application_provider_arn: "arn:aws:sso::aws:applicationProvider/custom"
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}

resource:
  aws_ssoadmin_application_access_scope:
    example:
      application_arn: ${aws_ssoadmin_application.example.arn}
      authorized_targets: 
        - "arn:aws:sso::123456789012:application/ssoins-123456789012/apl-123456789012"
      scope: "sso:account:access"
```
