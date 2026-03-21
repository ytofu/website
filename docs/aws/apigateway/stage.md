# API Gateway Stage

Create deployment stages using ytofu YAML.

## Basic Stage

```yaml
resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: prod
```

## With Logging

```yaml
resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: prod
      access_log_settings:
        destination_arn: ${aws_cloudwatch_log_group.example.arn}

  aws_api_gateway_method_settings:
    all:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: ${aws_api_gateway_stage.example.stage_name}
      method_path: "*/*"
      settings:
        metrics_enabled: true
        logging_level: INFO
        data_trace_enabled: true
```

## With Variables

```yaml
resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: prod
      variables:
        vpc_link_id: ${aws_api_gateway_vpc_link.example.id}
      tags:
        Environment: production
```
