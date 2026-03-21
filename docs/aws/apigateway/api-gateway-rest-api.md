# Resource: aws_api_gateway_rest_api

Manages an API Gateway REST API. The REST API can be configured via [importing an OpenAPI specification](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-import-api.html) in the `body` argument (with other arguments serving as overrides) or via other ytofu resources to manage the resources ([`aws_api_gateway_resource` resource](api_gateway_resource.html)), methods ([`aws_api_gateway_method` resource](api_gateway_method.html)), integrations ([`aws_api_gateway_integration` resource](api_gateway_integration.html)), etc. of the REST API. Once the REST API is configured, the [`aws_api_gateway_deployment` resource](api_gateway_deployment.html) can be used along with the [`aws_api_gateway_stage` resource](api_gateway_stage.html) to publish the REST API.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      body: '{ "openapi": "3.0.1" "info": { "title": "example" "version": "1.0" } "paths": { "/path1" = { "get": { x-amazon-apigateway-"integration": { "httpMethod": "GET" "payloadFormatVersion": "1.0" "type": "HTTP_PROXY" "uri": "https://ip-ranges.amazonaws.com/ip-ranges.json" } } } } }'
      name: example
      endpoint_configuration:
        types: 
          - REGIONAL

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

## OpenAPI Specification with Private Endpoints

```yaml
data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

  aws_region:
    current:

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16
      enable_dns_support: true
      enable_dns_hostnames: true

  aws_default_security_group:
    example:
      vpc_id: ${aws_vpc.example.id}

  aws_subnet:
    example:
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      cidr_block: 10.0.1.0/24
      vpc_id: ${aws_vpc.example.id}

  aws_vpc_endpoint:
    example:
      private_dns_enabled: false
      security_group_ids: 
        - ${aws_default_security_group.example.id}
      service_name: "com.amazonaws.${data.aws_region.current.region}.execute-api"
      subnet_ids: 
        - ${aws_subnet.example.id}
      vpc_endpoint_type: Interface
      vpc_id: ${aws_vpc.example.id}

  aws_api_gateway_rest_api:
    example:
      body: '{ "openapi": "3.0.1" "info": { "title": "example" "version": "1.0" } "paths": { "/path1" = { "get": { x-amazon-apigateway-"integration": { "httpMethod": "GET" "payloadFormatVersion": "1.0" "type": "HTTP_PROXY" "uri": "https://ip-ranges.amazonaws.com/ip-ranges.json" } } } } }'
      name: example
      put_rest_api_mode: merge
      endpoint_configuration:
        types: 
          - PRIVATE
        vpc_endpoint_ids: 
          - ${aws_vpc_endpoint.example[0].id}
          - ${aws_vpc_endpoint.example[1].id}
          - ${aws_vpc_endpoint.example[2].id}

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
* `api_key_source` - (Optional) Source of the API key for requests. Valid values are `HEADER` (default) and `AUTHORIZER`. If importing an OpenAPI specification via the `body` argument, this corresponds to the [`x-amazon-apigateway-api-key-source` extension](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-api-key-source.html). If the argument value is provided and is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `binary_media_types` - (Optional) List of binary media types supported by the REST API. By default, the REST API supports only UTF-8-encoded text payloads. If importing an OpenAPI specification via the `body` argument, this corresponds to the [`x-amazon-apigateway-binary-media-types` extension](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-binary-media-types.html). If the argument value is provided and is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `body` - (Optional) OpenAPI specification that defines the set of routes and integrations to create as part of the REST API. This configuration, and any updates to it, will replace all REST API configuration except values overridden in this resource configuration and other resource updates applied after this resource but before any `aws_api_gateway_deployment` creation. More information about REST API OpenAPI support can be found in the [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-import-api.html).
* `description` - (Optional) Description of the REST API. If importing an OpenAPI specification via the `body` argument, this corresponds to the `info.description` field. If the argument value is provided and is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `disable_execute_api_endpoint` - (Optional) Whether clients can invoke your API by using the default execute-api endpoint. By default, clients can invoke your API with the default https://{api_id}.execute-api.{region}.amazonaws.com endpoint. To require that clients use a custom domain name to invoke your API, disable the default endpoint. Defaults to `false`. If importing an OpenAPI specification via the `body` argument, this corresponds to the [`x-amazon-apigateway-endpoint-configuration` extension `disableExecuteApiEndpoint` property](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-endpoint-configuration.html). If the argument value is `true` and is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `endpoint_configuration` - (Optional) Configuration block defining API endpoint configuration including endpoint type. Defined below.
* `minimum_compression_size` - (Optional) Minimum response size to compress for the REST API. String containing an integer value between `-1` and `10485760` (10MB). `-1` will disable an existing compression configuration, and all other values will enable compression with the configured size. New resources can simply omit this argument to disable compression, rather than setting the value to `-1`. If importing an OpenAPI specification via the `body` argument, this corresponds to the [`x-amazon-apigateway-minimum-compression-size` extension](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-openapi-minimum-compression-size.html). If the argument value is provided and is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `name` - (Required) Name of the REST API. If importing an OpenAPI specification via the `body` argument, this corresponds to the `info.title` field. If the argument value is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `fail_on_warnings` - (Optional) Whether warnings while API Gateway is creating or updating the resource should return an error or not. Defaults to `false`
* `parameters` - (Optional) Map of customizations for importing the specification in the `body` argument. For example, to exclude DocumentationParts from an imported API, set `ignore` equal to `documentation`. Additional documentation, including other parameters such as `basepath`, can be found in the [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-import-api.html).
* `policy` - (Optional) JSON formatted policy document that controls access to the API Gateway. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy). ytofu will only perform drift detection of its value when present in a configuration. We recommend using the `aws_api_gateway_rest_api_policy` resource instead. If importing an OpenAPI specification via the `body` argument, this corresponds to the [`x-amazon-apigateway-policy` extension](https://docs.aws.amazon.com/apigateway/latest/developerguide/openapi-extensions-policy.html). If the argument value is provided and is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `put_rest_api_mode` - (Optional) Mode of the PutRestApi operation when importing an OpenAPI specification via the `body` argument (create or update operation). Valid values are `merge` and `overwrite`. If unspecificed, defaults to `overwrite` (for backwards compatibility). This corresponds to the [`x-amazon-apigateway-put-integration-method` extension](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-put-integration-method.html). If the argument value is provided and is different than the OpenAPI value, the argument value will override the OpenAPI value.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

**Note**: If the `body` argument is provided, the OpenAPI specification will be used to configure the resources, methods and integrations for the Rest API. If this argument is provided, the following resources should not be managed as separate ones, as updates may cause manual resource updates to be overwritten:

* `aws_api_gateway_resource`
* `aws_api_gateway_method`
* `aws_api_gateway_method_response`
* `aws_api_gateway_method_settings`
* `aws_api_gateway_integration`
* `aws_api_gateway_integration_response`
* `aws_api_gateway_gateway_response`
* `aws_api_gateway_model`

### endpoint_configuration

* `ip_address_type` - (Optional) The IP address types that can invoke an API (RestApi). Valid values: `ipv4`, `dualstack`. Use `ipv4` to allow only IPv4 addresses to invoke an API, or use `dualstack` to allow both IPv4 and IPv6 addresses to invoke an API. For the `PRIVATE` endpoint type, only `dualstack` is supported. ytofu performs drift detection for this argument only when the value is provided.
* `types` - (Required) List of endpoint types. This resource currently only supports managing a single value. Valid values: `EDGE`, `REGIONAL` or `PRIVATE`. If unspecified, defaults to `EDGE`. If set to `PRIVATE` recommend to set `put_rest_api_mode` = `merge` to not cause the endpoints and associated Route53 records to be deleted. Refer to the [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/create-regional-api.html) for more information on the difference between edge-optimized and regional APIs.
* `vpc_endpoint_ids` - (Optional) Set of VPC Endpoint identifiers. It is only supported for `PRIVATE` endpoint type. If importing an OpenAPI specification via the `body` argument, this corresponds to the [`x-amazon-apigateway-endpoint-configuration` extension `vpcEndpointIds` property](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-endpoint-configuration.html). If the argument value is provided and is different than the OpenAPI value, **the argument value will override the OpenAPI value**.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN
* `created_date` - Creation date of the REST API
* `execution_arn` - Execution ARN part to be used in `lambda_permission`'s `source_arn`
  when allowing API Gateway to invoke a Lambda function,
  e.g., `arn:aws:execute-api:eu-west-2:123456789012:z4675bid1j`, which can be concatenated with allowed stage, method and resource path.
* `id` - ID of the REST API
* `root_resource_id` - Resource ID of the REST API's root
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_api_gateway_rest_api.example 12345abcde
```
