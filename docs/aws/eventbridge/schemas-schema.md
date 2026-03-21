# Schemas Schema

Manage Schemas Schema resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_schemas_registry:
    test:
      name: my_own_registry

resource:
  aws_schemas_schema:
    test:
      name: my_schema
      registry_name: ${aws_schemas_registry.test.name}
      type: OpenApi3
      description: The schema definition for my event
      content: '{ "openapi" : "3.0.0", "info" : { "version" : "1.0.0", "title" : "Event" }, "paths" : {}, "components" : { "schemas" : { "Event" : { "type" : "object", "properties" : { "name" : { "type" : "string" } } } } } }'
```
