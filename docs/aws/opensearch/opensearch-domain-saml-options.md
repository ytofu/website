# Opensearch Domain SAML Options

Manage Opensearch Domain SAML Options resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      engine_version: OpenSearch_1.1
      cluster_config:
        instance_type: r4.large.search
      snapshot_options:
        automated_snapshot_start_hour: 23
      tags:
        Domain: TestDomain

resource:
  aws_opensearch_domain_saml_options:
    example:
      domain_name: ${aws_opensearch_domain.example.domain_name}
      saml_options:
        enabled: true
        idp:
          entity_id: "https://example.com"
          metadata_content: file-content
```
