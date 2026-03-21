# Resource: aws_servicecatalogappregistry_attribute_group

ytofu resource for managing an AWS Service Catalog AppRegistry Attribute Group.

## Basic Example

```yaml
resource:
  aws_servicecatalogappregistry_attribute_group:
    example:
      name: example
      description: example description
      attributes: '{ "app": "exampleapp" "group": "examplegroup" }'
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the Attribute Group.
* `attributes` - (Required) A JSON string of nested key-value pairs that represents the attributes of the group.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the Attribute Group.
* `tags` - (Optional) A map of tags assigned to the Attribute Group. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Attribute Group.
* `id` - ID of the Attribute Group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_servicecatalogappregistry_attribute_group.example 1234567890abcfedhijk09876s
```
