# Resource: aws_location_geofence_collection

ytofu resource for managing an AWS Location Geofence Collection.

## Basic Example

```yaml
resource:
  aws_location_geofence_collection:
    example:
      collection_name: example
```

## Argument Reference

The following arguments are required:

* `collection_name` - (Required) The name of the geofence collection.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) The optional description for the geofence collection.
* `kms_key_id` - (Optional) A key identifier for an AWS KMS customer managed key assigned to the Amazon Location resource.
* `tags` - (Optional) Key-value tags for the geofence collection. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `collection_arn` - The Amazon Resource Name (ARN) for the geofence collection resource. Used when you need to specify a resource across all AWS.
* `create_time` - The timestamp for when the geofence collection resource was created in ISO 8601 format.
* `update_time` - The timestamp for when the geofence collection resource was last updated in ISO 8601 format.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_location_geofence_collection.example example
```
