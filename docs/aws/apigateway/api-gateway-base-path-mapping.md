# API Gateway Base Path Mapping

Manage API Gateway Base Path Mapping resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example

resource:
  aws_api_gateway_domain_name:
    example:
      domain_name: example.com
      certificate_name: example-api
      certificate_body: file-content
      certificate_chain: file-content
      certificate_private_key: file-content

resource:
  aws_api_gateway_base_path_mapping:
    example:
      api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: ${aws_api_gateway_stage.example.stage_name}
      domain_name: ${aws_api_gateway_domain_name.example.domain_name}
```
