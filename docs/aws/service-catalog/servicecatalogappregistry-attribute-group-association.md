# Resource: aws_servicecatalogappregistry_attribute_group_association

ytofu resource for managing an AWS Service Catalog AppRegistry Attribute Group Association.

## Basic Example

```yaml
resource:
  aws_servicecatalogappregistry_application:
    example:
      name: example-app

  aws_servicecatalogappregistry_attribute_group:
    example:
      name: example
      description: example description
      attributes: '{ "app": "exampleapp" "group": "examplegroup" }'

  aws_servicecatalogappregistry_attribute_group_association:
    example:
      application_id: ${aws_servicecatalogappregistry_application.example.id}
      attribute_group_id: ${aws_servicecatalogappregistry_attribute_group.example.id}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_id` - (Required) ID of the application.
* `attribute_group_id` - (Required) ID of the attribute group to associate with the application.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_servicecatalogappregistry_attribute_group_association.example 12456778723424sdffsdfsdq34,12234t3564dsfsdf34asff4ww3
```
