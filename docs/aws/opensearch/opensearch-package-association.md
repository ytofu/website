# Opensearch Package Association

Manage Opensearch Package Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearch_domain:
    my_domain:
      domain_name: my-opensearch-domain
      engine_version: Elasticsearch_7.10
      cluster_config:
        instance_type: r4.large.search

resource:
  aws_opensearch_package:
    example:
      package_name: example-txt
      package_source:
        s3_bucket_name: ${aws_s3_bucket.my_opensearch_packages.bucket}
        s3_key: ${aws_s3_object.example.key}
      package_type: TXT-DICTIONARY

resource:
  aws_opensearch_package_association:
    example:
      package_id: ${aws_opensearch_package.example.id}
      domain_name: ${aws_opensearch_domain.my_domain.domain_name}
```
