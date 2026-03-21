# Resource: aws_opensearchserverless_collection

ytofu resource for managing an AWS OpenSearch Serverless Collection.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_security_policy:
    example:
      name: example
      type: encryption
      policy: '{ "Rules" = [ { "Resource" = [ "collection/example" ], "ResourceType" = "collection" } ], "AWSOwnedKey" = true }'

  aws_opensearchserverless_collection:
    example:
      name: example
      depends_on: 
        - ${aws_opensearchserverless_security_policy.example}```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the collection.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the collection.
* `standby_replicas` - (Optional) Indicates whether standby replicas should be used for a collection. One of `ENABLED` or `DISABLED`. Defaults to `ENABLED`.
* `tags` - (Optional) A map of tags to assign to the collection. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `type` - (Optional) Type of collection. One of `SEARCH`, `TIMESERIES`, or `VECTORSEARCH`. Defaults to `TIMESERIES`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the collection.
* `collection_endpoint` - Collection-specific endpoint used to submit index, search, and data upload requests to an OpenSearch Serverless collection.
* `dashboard_endpoint` - Collection-specific endpoint used to access OpenSearch Dashboards.
* `kms_key_arn` - The ARN of the Amazon Web Services KMS key used to encrypt the collection.
* `id` - Unique identifier for the collection.

## Timeouts

Configuration options:

- `create` - (Default `20m`)
- `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_opensearchserverless_collection.example example
```
