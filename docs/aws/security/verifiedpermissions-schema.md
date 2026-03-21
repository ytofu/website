# Verifiedpermissions Schema

Manage Verifiedpermissions Schema resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedpermissions_schema:
    example:
      policy_store_id: ${aws_verifiedpermissions_policy_store.example.policy_store_id}
      definition:
        value: '{ "Namespace" : { "entityTypes" : {}, "actions" : {} } }'
```
