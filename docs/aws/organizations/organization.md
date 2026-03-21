# AWS Organization

Create and manage an AWS Organization using ytofu YAML.

## Basic Organization

```yaml
resource:
  aws_organizations_organization:
    org:
      aws_service_access_principals:
        - cloudtrail.amazonaws.com
        - config.amazonaws.com
      feature_set: ALL
      enabled_policy_types:
        - SERVICE_CONTROL_POLICY
        - TAG_POLICY
```
