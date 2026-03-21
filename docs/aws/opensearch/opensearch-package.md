# Resource: aws_opensearch_package

Manages an AWS Opensearch Package.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    my_opensearch_packages:
      bucket: my-opensearch-packages

  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.my_opensearch_packages.bucket}
      key: example.txt
      source: ./example.txt
      etag: ${filemd5("./example.txt")}

  aws_opensearch_package:
    example:
      package_name: example-txt
      package_source:
        s3_bucket_name: ${aws_s3_bucket.my_opensearch_packages.bucket}
        s3_key: ${aws_s3_object.example.key}
      package_type: TXT-DICTIONARY```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `engine_version` - (Optional, Forces new resources) Engine version that the package is compatible with. This argument is required and only valid when `package_type` is `ZIP-PLUGIN`. Format: `OpenSearch_X.Y` or `Elasticsearch_X.Y`, where `X` and `Y` are the major and minor version numbers, respectively.
* `package_name` - (Required, Forces new resource) Unique name for the package.
* `package_type` - (Required, Forces new resource) The type of package. Valid values are `TXT-DICTIONARY`, `ZIP-PLUGIN`, `PACKAGE-LICENSE` and `PACKAGE-CONFIG`.
* `package_source` - (Required, Forces new resource) Configuration block for the package source options.
* `package_description` - (Optional, Forces new resource) Description of the package.

### package_source

* `s3_bucket_name` - (Required, Forces new resource) The name of the Amazon S3 bucket containing the package.
* `s3_key` - (Required, Forces new resource) Key (file name) of the package.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Id of the package.
* `available_package_version` - The current version of the package.

## Import

```bash
ytofu import aws_opensearch_package.example package-id
```
