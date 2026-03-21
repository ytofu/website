# Resource: aws_api_gateway_deployment

Manages an API Gateway REST Deployment. A deployment is a snapshot of the REST API configuration. The deployment can then be published to callable endpoints via the [`aws_api_gateway_stage` resource](api_gateway_stage.html) and optionally managed further with the [`aws_api_gateway_base_path_mapping` resource](api_gateway_base_path_mapping.html), [`aws_api_gateway_domain_name` resource](api_gateway_domain_name.html), and [`aws_api_method_settings` resource](api_gateway_method_settings.html). For more information, see the [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-deploy-api.html).

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      body: '{ "openapi": "3.0.1" "info": { "title": "example" "version": "1.0" } "paths": { "/path1" = { "get": { x-amazon-apigateway-"integration": { "httpMethod": "GET" "payloadFormatVersion": "1.0" "type": "HTTP_PROXY" "uri": "https://ip-ranges.amazonaws.com/ip-ranges.json" } } } } }'
      name: example

  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example```

## Terraform Resources

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: example

  aws_api_gateway_resource:
    example:
      parent_id: ${aws_api_gateway_rest_api.example.root_resource_id}
      path_part: example
      rest_api_id: ${aws_api_gateway_rest_api.example.id}

  aws_api_gateway_method:
    example:
      authorization: NONE
      http_method: GET
      resource_id: ${aws_api_gateway_resource.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}

  aws_api_gateway_integration:
    example:
      http_method: ${aws_api_gateway_method.example.http_method}
      resource_id: ${aws_api_gateway_resource.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      type: MOCK

  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the deployment.
* `rest_api_id` - (Required) REST API identifier.
* `triggers` - (Optional) Map of arbitrary keys and values that, when changed, will trigger a redeployment. To force a redeployment without changing these keys/values, use the `-replace` option with `ytofu plan` or `ytofu apply`.
* `variables` - (Optional) Map to set on the related stage.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the deployment
* `created_date` - Creation date of the deployment

## Import

```bash
ytofu import aws_api_gateway_deployment.example aabbccddee/1122334
```
