# Datazone Project

Manage Datazone Project resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datazone_project:
    test:
      domain_id: ${aws_datazone_domain.test.id}
      glossary_terms: 
        - 2N8w6XJCwZf
      name: name
      description: desc
      skip_deletion_check: true
```

## Basic Usage

```yaml
resource:
  aws_datazone_project:
    test:
      domain_identifier: ${aws_datazone_domain.test.id}
      name: name
```
