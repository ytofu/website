# Resource: aws_service_discovery_http_namespace

## Example Usage

## Basic Example

```yaml
resource:
  aws_service_discovery_http_namespace:
    example:
      name: development
      description: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the http namespace.
* `description` - (Optional) The description that you specify for the namespace when you create it.
* `tags` - (Optional) A map of tags to assign to the namespace. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of a namespace.
* `arn` - The ARN that Amazon Route 53 assigns to the namespace when you create it.
* `http_name` - The name of an HTTP namespace.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_service_discovery_http_namespace.example ns-1234567890
```
