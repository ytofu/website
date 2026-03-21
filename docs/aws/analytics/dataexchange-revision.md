# Resource: aws_dataexchange_revision

Provides a resource to manage AWS Data Exchange Revisions.

## Basic Example

```yaml
resource:
  aws_dataexchange_revision:
    example:
      data_set_id: ${aws_dataexchange_data_set.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `data_set_id` - (Required) The dataset id.
* `comment` - (Required) An optional comment about the revision.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Id of the data set.
* `revision_id` - The Id of the revision.
* `arn` - The Amazon Resource Name of this data set.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_dataexchange_revision.example 4fa784c7-ccb4-4dbf-ba4f-02198320daa1:4fa784c7-ccb4-4dbf-ba4f-02198320daa1
```
