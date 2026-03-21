# API Gateway Rest API

Manage API Gateway Rest API resources using ytofu YAML.

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

resource:
  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example
```

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

data:
  aws_region:
    current:

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16
      enable_dns_support: true
      enable_dns_hostnames: true

resource:
  aws_default_security_group:
    example:
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_subnet:
    example:
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      cidr_block: 10.0.1.0/24
      vpc_id: ${aws_vpc.example.id}

resource:
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

resource:
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

resource:
  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example
```

## Terraform Resources

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: example

resource:
  aws_api_gateway_resource:
    example:
      parent_id: ${aws_api_gateway_rest_api.example.root_resource_id}
      path_part: example
      rest_api_id: ${aws_api_gateway_rest_api.example.id}

resource:
  aws_api_gateway_method:
    example:
      authorization: NONE
      http_method: GET
      resource_id: ${aws_api_gateway_resource.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}

resource:
  aws_api_gateway_integration:
    example:
      http_method: ${aws_api_gateway_method.example.http_method}
      resource_id: ${aws_api_gateway_resource.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      type: MOCK

resource:
  aws_api_gateway_deployment:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      triggers:
        redeployment: example-value
      lifecycle:
        create_before_destroy: true

resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example
```
