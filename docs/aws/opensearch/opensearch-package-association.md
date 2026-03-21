# Resource: aws_opensearch_package_association

Manages an AWS Opensearch Package Association.

## Basic Example

```yaml
resource:
  aws_opensearch_domain:
    my_domain:
      domain_name: my-opensearch-domain
      engine_version: Elasticsearch_7.10
      cluster_config:
        instance_type: r4.large.search

  aws_opensearch_package:
    example:
      package_name: example-txt
      package_source:
        s3_bucket_name: ${aws_s3_bucket.my_opensearch_packages.bucket}
        s3_key: ${aws_s3_object.example.key}
      package_type: TXT-DICTIONARY

  aws_opensearch_package_association:
    example:
      package_id: ${aws_opensearch_package.example.id}
      domain_name: ${aws_opensearch_domain.my_domain.domain_name}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `package_id` - (Required, Forces new resource) Internal ID of the package to associate with a domain.
* `domain_name` - (Required, Forces new resource) Name of the domain to associate the package with.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Id of the package association.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)
