# Verifiedpermissions Policy

Manage Verifiedpermissions Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedpermissions_policy:
    test:
      policy_store_id: ${aws_verifiedpermissions_policy_store.test.id}
      definition:
        static:
          statement: "permit (principal, action == Action::\"view\", resource in Album:: \"test_album\");"
```
