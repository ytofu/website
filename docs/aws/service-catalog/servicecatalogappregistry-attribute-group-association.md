# Servicecatalogappregistry Attribute Group Association

Manage Servicecatalogappregistry Attribute Group Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicecatalogappregistry_application:
    example:
      name: example-app

resource:
  aws_servicecatalogappregistry_attribute_group:
    example:
      name: example
      description: example description
      attributes: '{ "app": "exampleapp" "group": "examplegroup" }'

resource:
  aws_servicecatalogappregistry_attribute_group_association:
    example:
      application_id: ${aws_servicecatalogappregistry_application.example.id}
      attribute_group_id: ${aws_servicecatalogappregistry_attribute_group.example.id}
```
