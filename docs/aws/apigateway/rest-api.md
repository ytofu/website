# API Gateway REST API

Create REST APIs using ytofu YAML.

## Basic REST API

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: MyDemoAPI
      description: This is my API for demonstration purposes
      endpoint_configuration:
        types:
          - REGIONAL
```

## With OpenAPI Spec

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: example
      body: example-json-policy
      endpoint_configuration:
        types:
          - REGIONAL
```

## Private API

```yaml
resource:
  aws_api_gateway_rest_api:
    example:
      name: private-api
      endpoint_configuration:
        types:
          - PRIVATE
        vpc_endpoint_ids:
          - ${aws_vpc_endpoint.example.id}
```

## REST API Policy

```yaml
resource:
  aws_api_gateway_rest_api_policy:
    example:
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      policy: ${data.aws_iam_policy_document.example.json}
```
