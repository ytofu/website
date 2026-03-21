# Resource: aws_api_gateway_rest_api_put

ytofu resource for updating an AWS API Gateway REST API with a new API description.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api_put:
    example:
      body: '{ "swagger": "2.0" "info": { "title": "Example API" "version": "v1" } "schemes": ["https"] "paths": { "/example" = { "get": { "responses": { "200" = { "description": "OK" } } x-amazon-apigateway-"integration": { "httpMethod": "GET" "type": "HTTP" "responses": { "default": { "statusCode": 200 } } "uri": "https://api.example.com/" } } } } }'
      fail_on_warnings: true
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
```

## Multi-stage

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: Example API

  aws_api_gateway_rest_api_put:
    examplev1:
      body: file-content
      fail_on_warnings: true
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

  aws_api_gateway_deployment:
    examplev1:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: ${aws_api_gateway_rest_api_put.examplev1.triggers.redeployment}
      lifecycle:
        create_before_destroy: true

  aws_api_gateway_stage:
    examplev1:
      stage_name: v1
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      deployment_id: ${aws_api_gateway_deployment.examplev1.id}

  aws_api_gateway_rest_api_put:
    examplev2:
      depends_on:
        - ${aws_api_gateway_stage.examplev1}
      body: file-content
      fail_on_warnings: true
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

  aws_api_gateway_deployment:
    examplev2:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: ${aws_api_gateway_rest_api_put.examplev2.triggers.redeployment}
      lifecycle:
        create_before_destroy: true

  aws_api_gateway_stage:
    examplev2:
      stage_name: v2
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      deployment_id: ${aws_api_gateway_deployment.examplev2.id}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `body` - (Required) PUT request body containing external API definitions. Currently, only OpenAPI definition JSON/YAML files are supported. The maximum size of the API definition file is 6MB.
* `rest_api_id` - (Required) Identifier of the associated REST API.

The following arguments are optional:

* `region` – (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `fail_on_warnings` - (Optional) Whether to rollback the API update when a warning is encountered. The default value is `false`.
* `parameters` - (Optional) Map of customizations for importing the specification in the `body` argument. For example, to exclude DocumentationParts from an imported API, use `ignore = "documentation"`. Additional documentation, including other parameters such as `basepath`, can be found in the [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-import-api.html).
* `triggers` - (Optional) Map of arbitrary keys and values that, when changed, will trigger a redeployment. To force a redeployment without changing these keys/values, use the `-replace` option with `ytofu plan` or `ytofu apply`.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `5m`)

## Import

```bash
ytofu import aws_api_gateway_rest_api_put.example import-id-12345678
```
