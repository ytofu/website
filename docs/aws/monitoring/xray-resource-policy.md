# Xray Resource Policy

Manage Xray Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_xray_resource_policy:
    test:
      policy_name: test
      policy_document: "{\"Version\":\"2012-10-17\",\"Statement\":[{\"Sid\":\"AllowXRayAccess\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":\"*\"},\"Action\":[\"xray:*\",\"xray:PutResourcePolicy\"],\"Resource\":\"*\"}]}"
      bypass_policy_lockout_check: true
```
