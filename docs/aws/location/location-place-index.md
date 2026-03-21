# Resource: aws_location_place_index

Provides a Location Service Place Index.

## Basic Example

```yaml
resource:
  aws_location_place_index:
    example:
      data_source: Here
      index_name: example
```

## Argument Reference

The following arguments are required:

* `data_source` - (Required) Specifies the geospatial data provider for the new place index.
* `index_name` - (Required) The name of the place index resource.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `data_source_configuration` - (Optional) Configuration block with the data storage option chosen for requesting Places. Detailed below.
* `description` - (Optional) The optional description for the place index resource.
* `tags` - (Optional) Key-value tags for the place index. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### data_source_configuration

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `intended_use` - (Optional) Specifies how the results of an operation will be stored by the caller. Valid values: `SingleUse`, `Storage`. Default: `SingleUse`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `create_time` - The timestamp for when the place index resource was created in ISO 8601 format.
* `index_arn` - The Amazon Resource Name (ARN) for the place index resource. Used to specify a resource across AWS.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `update_time` - The timestamp for when the place index resource was last update in ISO 8601.

## Import

```bash
ytofu import aws_location_place_index.example example
```
