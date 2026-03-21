# Resource: aws_api_gateway_model

Provides a Model for a REST API Gateway.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    MyDemoAPI:
      name: MyDemoAPI
      description: This is my API for demonstration purposes

  aws_api_gateway_model:
    MyDemoModel:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      name: user
      description: a JSON schema
      content_type: application/json
      schema: '{ "type": "object" }'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rest_api_id` - (Required) ID of the associated REST API
* `name` - (Required) Name of the model
* `description` - (Optional) Description of the model
* `content_type` - (Required) Content type of the model
* `schema` - (Required) Schema of the model in a JSON form

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the model

## Import

```bash
ytofu import aws_api_gateway_model.example 12345abcde/example
```
