# Resource: aws_apigatewayv2_model

Manages an Amazon API Gateway Version 2 [model](https://docs.aws.amazon.com/apigateway/latest/developerguide/models-mappings.html#models-mappings-models).

## Basic Example

```yaml
resource:
  aws_apigatewayv2_model:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      content_type: application/json
      name: example
      schema: '{ "$schema" = "http://json-schema.org/draft-04/schema#" "title": "ExampleModel" "type": "object" "properties": { "id": { "type": "string" } } }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `api_id` - (Required) API identifier.
* `content_type` - (Required)  The content-type for the model, for example, `application/json`. Must be between 1 and 256 characters in length.
* `name` - (Required) Name of the model. Must be alphanumeric. Must be between 1 and 128 characters in length.
* `schema` - (Required) Schema for the model. This should be a [JSON schema draft 4](https://tools.ietf.org/html/draft-zyp-json-schema-04) model. Must be less than or equal to 32768 characters in length.
* `description` - (Optional) Description of the model. Must be between 1 and 128 characters in length.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Model identifier.

## Import

```bash
ytofu import aws_apigatewayv2_model.example aabbccddee/1122334
```
