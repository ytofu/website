# Verifiedpermissions Policy Template

Manage Verifiedpermissions Policy Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedpermissions_policy_template:
    example:
      policy_store_id: ${aws_verifiedpermissions_policy_store.example.id}
      statement: "permit (principal in ?principal, action in PhotoFlash::Action::\"FullPhotoAccess\", resource == ?resource) unless { resource.IsPrivate };"
```
