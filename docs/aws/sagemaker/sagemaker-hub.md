# Resource: aws_sagemaker_hub

Provides a SageMaker AI Hub resource.

## Basic Example

```yaml
resource:
  aws_sagemaker_hub:
    example:
      hub_name: example
      hub_description: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `hub_name` - (Required) The name of the hub.
* `hub_description` - (Required) A description of the hub.
* `hub_display_name` - (Optional) The display name of the hub.
* `hub_search_keywords` - (Optional) The searchable keywords for the hub.
* `s3_storage_config` - (Optional) The Amazon S3 storage configuration for the hub. See [S3 Storage Config](#s3-storage-config) details below.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### S3 Storage Config

* `s3_output_path` - (Optional) The Amazon S3 bucket prefix for hosting hub content.interface.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the Hub.
* `arn` - The Amazon Resource Name (ARN) assigned by AWS to this Hub.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_sagemaker_hub.test_hub my-code-repo
```
