# API Gateway Usage Plan

Configure rate limiting and quotas using ytofu YAML.

## Basic Usage Plan

```yaml
resource:
  aws_api_gateway_usage_plan:
    example:
      name: my-usage-plan
      description: Usage plan with throttle and quota
      api_stages:
        - api_id: ${aws_api_gateway_rest_api.example.id}
          stage: ${aws_api_gateway_stage.example.stage_name}
      throttle_settings:
        burst_limit: 5
        rate_limit: 10
      quota_settings:
        limit: 1000
        offset: 0
        period: MONTH
```

## Usage Plan Key

```yaml
resource:
  aws_api_gateway_usage_plan_key:
    example:
      key_id: ${aws_api_gateway_api_key.example.id}
      key_type: API_KEY
      usage_plan_id: ${aws_api_gateway_usage_plan.example.id}
```
