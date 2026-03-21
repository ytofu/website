# Identitystore Group

Manage Identitystore Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_identitystore_group:
    this:
      display_name: Example group
      description: Example description
      identity_store_id: ${data.aws_ssoadmin_instances.example.identity_store_ids[0]}
```
