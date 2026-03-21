# Resource: aws_datapipeline_pipeline

Provides a DataPipeline Pipeline resource.

## Basic Example

```yaml
resource:
  aws_datapipeline_pipeline:
    default:
      name: tf-pipeline-default
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of Pipeline.
* `description` - (Optional) The description of Pipeline.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The identifier of the client certificate.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_datapipeline_pipeline.default df-1234567890
```
