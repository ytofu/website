# Cloudsearch Domain

Manage Cloudsearch Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudsearch_domain:
    example:
      name: example-domain
      scaling_parameters:
        desired_instance_type: search.medium
      index_field:
        name: headline
        type: text
        search: true
        return: true
        sort: true
        highlight: false
        analysis_scheme: _en_default_
      index_field:
        name: price
        type: double
        search: true
        facet: true
        return: true
        sort: true
        source_fields: headline
```
