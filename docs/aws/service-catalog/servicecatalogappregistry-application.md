# Resource: aws_servicecatalogappregistry_application

ytofu resource for managing an AWS Service Catalog AppRegistry Application.

## Basic Example

```yaml
resource:
  aws_servicecatalogappregistry_application:
    example:
      name: example-app
```

## Connecting Resources

```yaml
resource:
  aws_servicecatalogappregistry_application:
    example:
      name: example-app

  aws_s3_bucket:
    bucket:
      bucket: example-bucket
      tags: ${aws_servicecatalogappregistry_application.example.application_tag}```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the application. The name must be unique within an AWS region.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the application.
* `tags` - (Optional) A map of tags assigned to the Application. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `application_tag` - A map with a single tag key-value pair used to associate resources with the application. This attribute can be passed directly into the `tags` argument of another resource, or merged into a map of existing tags.
* `arn` - ARN (Amazon Resource Name) of the application.
* `id` - Identifier of the application.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_servicecatalogappregistry_application.example application-id-12345678
```
