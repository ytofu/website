# Workspacesweb Portal

Manage Workspacesweb Portal resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example-portal
      instance_type: standard.regular
```

## Complete Usage

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS key for WorkSpaces Web Portal
      deletion_window_in_days: 7

resource:
  aws_workspacesweb_portal:
    example:
      display_name: example-portal
      instance_type: standard.large
      authentication_type: IAM_Identity_Center
      customer_managed_key: ${aws_kms_key.example.arn}
      max_concurrent_sessions: 10
      additional_encryption_context:
        Environment: Production
      tags:
        Name: example-portal
      timeouts:
        create: 10m
        update: 10m
        delete: 10m
```
