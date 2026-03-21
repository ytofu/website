# API Gateway Usage Plan Key

Manage API Gateway Usage Plan Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    test:
      name: MyDemoAPI

resource:
  aws_api_gateway_usage_plan:
    myusageplan:
      name: my_usage_plan
      api_stages:
        api_id: ${aws_api_gateway_rest_api.test.id}
        stage: ${aws_api_gateway_stage.foo.stage_name}

resource:
  aws_api_gateway_api_key:
    mykey:
      name: my_key

resource:
  aws_api_gateway_usage_plan_key:
    main:
      key_id: ${aws_api_gateway_api_key.mykey.id}
      key_type: API_KEY
      usage_plan_id: ${aws_api_gateway_usage_plan.myusageplan.id}
```
