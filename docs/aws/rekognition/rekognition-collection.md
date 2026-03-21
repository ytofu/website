# Resource: aws_rekognition_collection

ytofu resource for managing an AWS Rekognition Collection.

## Basic Example

```yaml
resource:
  aws_rekognition_collection:
    example:
      collection_id: my-collection
      tags:
        example: 1
```

## Argument Reference

The following arguments are required:

* `collection_id` - (Required) The name of the collection

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Collection.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `face_model_version` - The Face Model Version that the collection was initialized with

## Timeouts

Configuration options:

- `create` - (Default `2m`)

## Import

```bash
ytofu import aws_rekognition_collection.example collection-id-12345678
```
