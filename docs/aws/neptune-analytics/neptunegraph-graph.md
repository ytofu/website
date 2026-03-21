# Neptunegraph Graph

Manage Neptunegraph Graph resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_neptunegraph_graph:
    example:
      graph_name: example-graph-test-20250203
      provisioned_memory: 16
      deletion_protection: false
      public_connectivity: false
      replica_count: 1
      kms_key_identifier: "arn:aws:kms:us-east-1:123456789012:key/12345678-1234-1234-1234-123456789012"
      vector_search_configuration:
        vector_search_dimension: 128
      tags: 
```
