# Keyspaces Table

Manage Keyspaces Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_keyspaces_table:
    example:
      keyspace_name: ${aws_keyspaces_keyspace.example.name}
      table_name: my_table
      schema_definition:
        column:
          name: Message
          type: ASCII
        partition_key:
          name: Message
```
